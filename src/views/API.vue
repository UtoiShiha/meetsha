<template>
  <div class="api">
        <p>真夏の夜の.incが誇る超高性能AIとお話しよう！</p>
        <input type="text" v-model="text" v-on:keyup.enter="getRes(text)"/>
        <p v-if="mode == 0"><img src="https://twemoji.maxcdn.com/2/72x72/1f600.png" alt=""></p>
        <p v-if="mode == 1"><img src="https://twemoji.maxcdn.com/2/72x72/1f914.png" alt=""></p>
        <p>{{res}}</p>

        <p>{{users}}</p>
        <svg width="100%" height="300%">
            <circle :r="r" cx="150" cy="75" stroke="black" stroke-width="1" fill="fill" />
        </svg>
        <button v-on:click="feed()">育てる</button>
        
        <p><button v-on:click="getNeetInfo()">NeetSha</button></p>
        <ul id="example-1">
            <li v-for="item in record">
                <a :href="item.link"><img :src="item.thumb" alt=""></a><br>
                {{item.title}}<br>{{item.author}}
            </li>
        </ul>
  </div>
</template>

<script>
export default {
    name: 'api',
    data(){
      return{
          users:"",
          text:"",
          baseURI:"https://jlp.yahooapis.jp/NLUService/V1/analyze?appid=dj00aiZpPUZ4aU8xRTVwM1lmMyZzPWNvbnN1bWVyc2VjcmV0Jng9NTM-&intext=",
          response:"",
          res:"",
          mode:0,
          r:5,
          neet:"",
          test:[],
          record:[]          
      }
    },
    mounted(){
        this.getNeetInfo();
    },
    methods:{
        getRes(text){
            this.$http.get(this.baseURI+text)
                .then((result) => {
                    this.users = result.data;
                    if(result.data.result.hasOwnProperty('param_text')){
                        this.res = result.data.result.param_text;
                        this.mode = 0;
                    }else{
                        this.res = "会話になってねぇよ"
                                                this.mode = 1;
                    }
                })
        },
        getNeetInfo(){
            this.record=[];
            let url = "http://neetsha.jp/inside/api/v0/comic.php";
            this.$http.get(url).then(result => {
                    let test ="aa";
                    this.neet = result.data.split('\n',50);
                    let count =0;
                    this.neet.forEach(element => {
                        let buffer = element.split("\t");
                        if(buffer[0] == 0){return;}
                        let record={};
                        record.id = buffer[0];
                        record.code = buffer[1];
                        record.title = buffer[2];
                        record.link = "http://neetsha.in/"+buffer[0];
                        record.author = buffer[5];
                        if(buffer[buffer.length - 2] != ""){
                            record.thumb = "http://neetsha.jp/inside/up/"+record.id.slice(0,1)+"/"+record.id.slice(1,2)+"/"+record.id+"/"+buffer[buffer.length - 2];
                        }else{
                             record.thumb = "http://neetel.neetsha.com/image/default_thumb.gif";
                        }
                        record.update = buffer[buffer.length - 1];
                        this.record.push(record);
                    });
            });
        },
        feed(){
            this.r += 5;
        }
  }
}
</script>

<style>
    li{
        list-style: none;
        float:left;
        display: inline-block;
        width: 30%;
        overflow: hidden;
    }
</style>