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
        <div class="col-md-2">
          <ul>
            <li v-for="todo in todos" :key="todo.id">
              <h2
                @click="toggleDone(todo)"
                :class="{ done: todo.done }"
                class="todo"
              >
                {{ todo.content }}
              </h2>
            </li>
          </ul>
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

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    // makes it so you have access in the template
    return {
      toggleDone,
      todos,
      newTodo,
      createTodo,
    };
  },
};
</script>

<style>
.done {
  text-decoration: line-through;
}
.todo {
  cursor: pointer;
}
</style>