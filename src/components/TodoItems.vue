<template>
  <div class="todo-item" v-bind:class="{'completed':todo.completed}">
    <p>
      <input type="checkbox" v-on:change="markComplete">
      {{todo.title}}
      <button @click="$emit('del-todo', todo.id)" class="delete">Delete</button>
      </p>
  </div>
</template>

<script>
export default {
  name: "TodoItems",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
      }
    }
}
</script>

<style scoped>
  .todo-item {
    background: black;
    padding: 10px;
    border-bottom: 1px solid grey;
    }
    .completed {
        text-decoration: strikethrough;
      }
      .delete {

      }
</style>
