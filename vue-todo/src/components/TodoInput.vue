<template>
  <div>
      <!-- template에 들어가는 태그는 하나만 존재할수있다 -->
      <input type="text" v-model="newTodoItem">
      <button v-on:click="addTodo">add</button>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      newTodoItem: ""
    }
  },
  methods: {
    addTodo: function(){
      console.log(this.newTodoItem);
      localStorage.setItem(this.newTodoItem ,this.newTodoItem);
      this.newTodoItem = '';
    
    }
  }
}
</script>

<style>

</style>