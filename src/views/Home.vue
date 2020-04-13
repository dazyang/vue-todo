<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteItem" />
  </div>
</template>

<script>
import Todos from '../components/Todos.vue'
import AddTodo from '../components/AddTodo.vue'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  data () {
    return {
      todos: []
    }
  },
  methods: {
    // taking id as a payload
    deleteItem (id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(
          res =>
            (this.todos = this.todos.filter(todo => todo.id !== id, res.data))
        )
        .catch(err => console.log('Ah no -----> ' + err))
    },
    addTodo (newTodo) {
      const { title, completed } = newTodo
      // making a http post request to API and the object data we are sending
      axios
        .post('https://jsonplaceholder.typicode.com/todos', {
          title: title,
          completed: completed
        })
        // the request returns (a promise) back the todo along with the id it generated
        .then(res => (this.todos = [...this.todos, res.data]))
        .catch(err => console.log(err))
    }
  },
  // created is similar to componentDidMount in React, fires off when component loads
  created () {
    // making an http get request to a backend API
    axios
      .get('https://jsonplaceholder.typicode.com/todos?_limit=8')
      // resolving the returned promise, it gives a response back
      .then(res => (this.todos = res.data))
      // catch an error
      .catch(err => console.log('What the heck is going on? ---> ' + err))
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 1%;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
  color: white;
  background-color: grey;
}
button {
  border-style: none;
}
</style>
