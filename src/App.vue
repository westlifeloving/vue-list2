<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo"/>
    <SearchTodo v-on:search-todo="filteredTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Header from './components/layout/Header.vue';
import Todos from './components/Todos.vue';
import AddTodo from './components/AddTodo.vue';
import SearchTodo from './components/SearchTodo.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Header,
    Todos,
    AddTodo,
    SearchTodo
  },
  data(){
    return{
      todos:[]
    }
  },
  methods:{
    deleteTodo(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
        .catch(err => console.log(err));

    },
    addTodo(newTodo){
      const { title, completed } = newTodo;

      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));
    },
    filteredTodo:function() {
      let filList= this.todos.filter(todo => {
        return todo.title.match(this.search);
        });
    }
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(res => this.todos = res.data)
      .catch(err => console.log(err));
  }
}
</script>

<style>
 *{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
 }

 body{
  font-family: Arial, Helvetica, sans-serif;
  font-size: 14px;
  line-height: 2;
 }

 .btn{
  display: inline-block;
  border: none;
  background: #dc9090;
  color: #333;
  padding: 7px 20px;
  cursor: pointer;
 }

 .btn:hover{
  background: #eee;
 }
</style>
