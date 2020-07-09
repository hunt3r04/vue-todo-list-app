<template>
  <div id="app">
    <Todos v-bind:todos="todos" v-on:del-todo="delTodo"/>
  </div>
</template>

<script>
import Todos from './components/Todos';

export default {
  name: 'App',
  components: {
    Todos
  },
  data(){
    return{
     todos: [
       {
         id:1,
         title:"Todo 1",
         completed: false
       },
       {
         id:2,
         title:"Todo 2",
         completed: false
       },
       {
         id:3,
         title:"Todo 3",
         completed: false
       },{
         id:4,
         title:"Todo 4",
         completed: false
       },
      ]
    }
  },
  methods:{
    delTodo(id){
      this.todos = this.todos.filter(todo => todo.id !== id);
    }
  }
}
</script>

<style>
* {
  padding: 0;
  margin :0;
}

body{
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
</style>
