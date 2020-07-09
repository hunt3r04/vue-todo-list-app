<template>
  <div id="app">
    <Header/>
    <div class="container">
    <br>
      <AddTodo v-on:addtodo="addTodo" />
      <br>
     <div class="card">
       <Todos v-bind:todos="todos" v-on:del-todo="delTodo"/>
     </div>
    </div>
  </div>
</template>

<script>
import Todos from '../components/Todos';
import Header from '../components/layout/header'
import AddTodo from '../components/AddTodo'
import axios from 'axios'
export default {
  name: 'Home',
  components: {
    Todos,
    Header,
    AddTodo
  },
  data(){
    return{
     todos: [
      
      ]
    }
  },
  methods:{
    delTodo(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(err => console.log(err));
      
    },
    addTodo(newTodo){
      const { title, completed} = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title,
        completed
      })
      .then(res => this.todos = [...this.todos, res.data] )
      .catch(err =>console.log(err));
     // this.todos = [...this.todos, newTodo];
    }
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res => this.todos = res.data)
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
.btn{
  display: inline-block;
  border: none !important;
  border-radius:0px !important;
  background:#555;
  color:#fff;
  cursor: pointer;;
}

.btn:hover{
  background: #666;
}
</style>
