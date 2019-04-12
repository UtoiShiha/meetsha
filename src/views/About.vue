<template>
  <div class="about">
    <h1>Hello,Vue</h1>
    <p v-if="msg.length > 0">
      {{msg}}
    </p>
    <p v-else>
      no text
    </p>
    <input type="text" v-model="msg">
    <button @click="clear()">clear</button>
  </div>
</template>

<script>
export default {
    name: 'about',
    data(){
      return{
        msg: 'Hellor Vue.js!'
      }
    },
    methods:{
    clear(){
      this.msg = ''
    }
  }
}
</script>
