<template>
<h1>TEST COMPONENT {{text}}</h1>
  <h3 v-for="item of items" v-bind:key="item.id">
    {{item.text}} <button v-on:click="removeItem(item.id)">remove</button>
  </h3>
</template>

<script>
export default {
  name: "Test",
  /*props:['text']*/
  props:{
    items:{
      type:Array,
      required:true
    }
  },
  methods:{
    removeItem(id){
      this.$emit('removeItem',id)
      //this.items=this.items.filter(item=>item.id!==id)
      console.log(id)
    },
  },
  emits:['removeItem']
}
</script>

<style scoped>

</style>
