<template>
  <div class="todo-component">
    <div class="container-fluid">
      <div class="row">
        <div class="col-md-12">
          <form @submit.prevent="createTodo">
            <label for="todo">Enter Todo Here:</label>
            <input
              type="text"
              name="newTodo"
              placeholder="Enter Todo Here..."
              v-model="newTodo"
            />
            <button class="btn btn-success" type="submit">Submit Todo</button>
          </form>
        </div>
      </div>
    </div>
    <div class="container-fluid">
      <div class="row">
        <div class="col-md-12" v-for="todo in todos" :key="todo.id">
          {{ todo.content }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// reactive variable that keeps track of what the user has input { ref } Reusable outside of Vue.js, variables objects respond to change
import { ref } from "vue";
export default {
  name: "todo-component",
  setup() {
    // object wrapper, property called value on it
    const newTodo = ref("");
    const todos = ref([]);

    function createTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }
    // makes it so you have access in the template
    return {
      todos,
      newTodo,
      createTodo,
    };
  },
};
</script>

<style>
</style>