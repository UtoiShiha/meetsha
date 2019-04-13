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
    <p>{{ counter }}</p>
    <button v-on:click="add">追加（関数）</button>
    <button v-on:click="counter++">追加（JavaScriptの文）</button><p>
    <input type="text"
      placeholder="TODOを入力しましょう！"
      v-model="newItemTitle"
      v-on:keyup.enter="addTodo(newItemTitle)"></p>
      
  <button v-on:click="deleteTodo()">チェック済みの項目を削除する</button>
    <ul>
      <li v-for="item in items">
        <label v-bind:class="{ done: item.isChecked }">
          <input type="checkbox" v-model="item.isChecked"> {{ item.title }}
        </label>
      </li>
    </ul>
   
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
        items: [
            { title: '領収書を準備する', isChecked: true },
            { title: 'Vue.jsハンズオンの資料を作る', isChecked: true },
            { title: '参加者の人数を確認する', isChecked: false },
            { title: 'ピザを注文する', isChecked: false },
            { title: '参加費のお釣りを準備する', isChecked: false },
            { title: '会場設営をする', isChecked: false },
        ],
        newItemTitle: '', //追加
        counter: 0,
      }
    },
    mounted(){
    this.loadTodo();
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
    ,add(){
      this.counter++
    },addTodo(newTitle){
      this.items.push({
        title: newTitle,
        isChecked: false
      });
      this.newItemTitle = '';
      this.saveTodo(); //ブラウザに保存
    },deleteTodo(){
      this.items = this.items.filter(function (item) {
        return item.isChecked === false; //
      });
      this.saveTodo(); //ブラウザに保存
    },saveTodo: function(){
      localStorage.setItem('items', JSON.stringify(this.items));
    }, loadTodo: function(){
      this.items = JSON.parse( localStorage.getItem('items') );
      if( !this.items ){
        this.items = [];
      }
    },
  }
}
</script>

<style>
  .done { text-decoration: line-through; }
</style>