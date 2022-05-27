<template>

  <button v-on:click="isVisible=!isVisible">togle list visibility ({{isVisible}})</button>

  <Test v-if="isVisible" v-bind:items="items" v-on:removeItem="removeItemFromList"/>
  <h1 v-else-if="!isVisible && counter===0">some strange condition</h1>
  <h1 v-else>list is hidden</h1>

  <img alt="Vue logo" src="./assets/logo.png">

  <h1>{{user.name}}</h1>
  <div>counter value :{{counter}}</div>
  <button v-on:click="incCounter($event,123)" >inc</button>
  <button v-on:click="decCounter($event,123)" >dec</button>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Test from './components/Test.vue'

export default {
  name: 'App',
  data() {
    return{
      isVisible:true,
      items:[{id:1,text:"text1"},{id:2,text:"text2"},{id:3,text:"text3"}],
      counter:0,
      userName:'andriy',
      user:{
        name:'lol'
      }
    }
  },
  methods:{
    removeItemFromList(id){
      this.items=this.items.filter(item=>item.id!==id)

  },
    incCounter(){
      this.counter++
      this.user.name += this.counter
    },
    decCounter(name){
      this.counter--
    }
  },
  components: {
    /*HelloWorld,*/
    Test
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
