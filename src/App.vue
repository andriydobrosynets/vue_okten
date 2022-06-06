<template>
  <form v-on:submit="onSubmit">
    <input type="text" v-model="inputValue">
    <!--v-bind:value="inputValue" v-on:input="inputValue=$event.target.value"-->
    <input type="checkbox" v-model="isVisible">
    <h1>{{inputValue}}</h1>
    <button>submit</button>
  </form>



  <button v-on:click="isVisible=!isVisible">togle list visibility ({{isVisible}})</button><br>

  <button v-on:click="currentPage=currentPage-1">prev page</button>
  <button >current page{{currentPage}}</button>
  <button v-on:click="currentPage=currentPage+1">next page</button>

  <TestWorld v-if="isVisible" v-bind:items="items" v-on:removeItem="removeItemFromList"/>
  <h1 v-else-if="!isVisible && counter===0">some strange condition</h1>
  <h1 v-else>list is hidden</h1>
<!--  <HelloWorld/>-->
  <img alt="Vue logo" src="./assets/logo.png">

  <h1>{{user.name}}</h1>
  <div v-bind:style="`font-size:${counter*10}px`" v-bind:class="{test:counter%2===0}">counter value :{{counter}}</div>
  <button v-on:click="incCounter($event,123)" >inc</button>
  <button v-on:click="decCounter($event,123)" >dec</button>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
/*import Test from './components/TestWorld.vue'*/
import TestWorld from "@/components/TestWorld.vue";

export default {
  name: 'App',
  created() {
    this.getTodos();
    console.log("test created")
  },
  mounted() {
    console.log("test mounted")
  },
  /*updated() {
    this.getTodos();
  },*/
  watch:{
    currentPage(){
      this.getTodos()
    }
  },
  data() {
    return{
      inputValue:'',
      pageSize:10,
      currentPage:1,
      isVisible:true,
      items:[],
      counter:0,
      userName:'andriy',
      user:{
        name:'lol'
      }
    }
  },
  methods:{
    onSubmit(event){
      event.preventDefault()
      console.log(this.inputValue, this.isVisible)
    },
    removeItemFromList(id){
      this.items=this.items.filter(item=>item.id!==id)

  },
    incCounter(){
      this.counter++
      this.user.name += this.counter
    },
    decCounter(){
      this.counter--
    },
    async getTodos(){
      const limit = this.currentPage*this.pageSize
      const response = await fetch(`https://jsonplaceholder.typicode.com/todos?_limit=${limit}`)
      const data = await response.json();
      console.log(data)
      this.items=data
    }
  },
  components: {
    TestWorld,

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
.test{
  background: cornflowerblue;
}
</style>
