<template>
  <div class="about">
    <h1>真夏の夜の.inc</h1>
    <p v-if="msg.length > 0">
      {{msg}}
    </p>
    <p v-else>
      no text
    </p>
    <input type="text" v-model="msg">
    <button @click="clear()">clear</button>
    <br>
    
    <p v-if="msg.length > 0">
          <button @click="test()">中日の次の試合は。。。？</button>
    </p>
    <p>{{unchi}}</p>
    <p>w{{winCount}}:l{{loseCount}}</p>
  </div>
</template>

<script>
export default {
    name: 'about',
    data(){
      return{
        msg: 'margarineちゃんのえっちないえ',
        unchi:'',
        winCount:0,
        loseCount:0,
      }
    },
    methods:{
    clear(){
      this.msg = ''
    },
    test(){
      let max = 10;
      let min = 0;
      let num =  Math.random() * (max - min) + min;
      if(num > 5){
        this.unchi='勝ち！w'
        this.winCount++;
      }else{
        this.unchi='負け！w'
        this.loseCount++;
      }
    }
  }
}
</script>
