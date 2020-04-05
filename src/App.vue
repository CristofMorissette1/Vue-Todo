<template>
  <div id="app">
    <Header />
    <NewTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>
  
<script>
import Todos from './components/TodosList';
import Header from './components/layout/Header';
import NewTodo from './components/NewTodo';
import axios from 'axios';
export default {
  name: 'App',
  components: {
    Todos,
    Header,
    NewTodo
  },
  data() {
    return {
      todos: []
    }
  },
    mounted() {
      if (localStorage.todos) {
        this.todos = JSON.parse(localStorage.todos);
      } 
      else if (!localStorage.todos) {
        axios.get('https://jsonplaceholder.typicode.com/todos?_limit=3')
        .then(res => this.todos = res.data)
        .catch(err => console.log(err))
      }
    },
    watch: {
      todos: {
        handler(savedTodos) {
          localStorage.todos = JSON.stringify(savedTodos);
        },
        deep: true
      }
    },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => this.todos = this.todos.filter(todo => todo.id !== id, res.data))
        .catch(err => console.log(err));
    }, 
    addTodo(newTodo) {
      let { title, completed } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        .then(res =>this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));
    }
  }
}
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
