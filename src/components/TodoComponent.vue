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
        <div class="col-md-4">
          <ul>
            <li v-for="(todo, index) in todos" :key="todo.id">
              <div class="d-flex justify-content-between">
                <h4
                  @click="toggleDone(todo)"
                  :class="{ done: todo.done }"
                  class="todo"
                >
                  {{ todo.content }}
                </h4>
                <button
                  class="btn btn-danger btn-sm"
                  @click="removeTodo(index)"
                >
                  Delete
                </button>
              </div>
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

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    // makes it so you have access in the template
    return {
      removeTodo,
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