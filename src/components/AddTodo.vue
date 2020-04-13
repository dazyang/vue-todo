<template>
  <div>
    <!-- set to a method called addTodo -->
    <form @submit="addTodo">
      <!-- v-model directive bounded to title -->
      <input type="text" v-model="title" name="title" placeholder="Add Todo...">
      <input type="submit" value="Submit" class="button">
    </form>
  </div>
</template>

<script>
// import uuid from 'uuid'; 
export default {
  name: "AddTodo",
  data() {
    // return an object
    return {
      title: ''
    } 
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      // construct an object
      const newTodo = {
        // id: uuid.v4(),
        // this checking v-model
        title: this.title,
        completed: false
      }
      // send up to parent
      this.$emit('add-todo', newTodo) 
      this.title = ''
    }
  }
}
</script>

<style scoped>
form {
  display: flex
}
input[type="text"] {
    flex: 10;
    padding: 5px;
}
input[type="submit"] {
  flex: 2;
}
</style>