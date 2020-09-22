<template>
  <div id="app">
    <Header />
    <AddToDo v-on:add-todo = "addToDo" />
    <Todos v-bind:todos = "todos" v-on:del-todo = "deleteTodo" />
  </div>
</template>

<script>
import Todos from "./components/Todos";
import Header from ".//components/layout/Header";
import AddToDo from ".//components/AddToDo";
import axios from 'axios'

export default {
  name: "App",

  components: {
    Todos,
     Header,
     AddToDo 
  },

  data() {
    return {
      todos: []
    }
  },

  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },

    addToDo(newTodo) {
      const { title, completed } = newTodo;
      axios.post("https://jsonplaceholder.typicode.com/todos", {
        title,
        completed 
      })
      .then(res =>  this.todos = [...this.todos, res.data])
      // .catch(err => console.log)

     ;
    }
  },

  created() {
    axios.get("https://jsonplaceholder.typicode.com/todos?_limit=10")
    .then(response => this.todos = response.data)
    .catch(err => console.log(err));
  }
};
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #666;
  }
</style>
