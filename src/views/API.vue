<template>
  <div class="api">
        <p>真夏の夜の.incが誇る超高性能AIとお話しよう！</p>
        <input type="text" v-model="text" v-on:keyup.enter="getRes(text)"/>
        <p v-if="mode == 0"><img src="https://twemoji.maxcdn.com/2/72x72/1f600.png" alt=""></p>
        <p v-if="mode == 1"><img src="https://twemoji.maxcdn.com/2/72x72/1f914.png" alt=""></p>
        <p>{{res}}</p>

        <!-- <p>{{users}}</p> -->
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
          mode:0
      }
    },
    mounted(){

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
  }
}
</script>

<style>
</style>