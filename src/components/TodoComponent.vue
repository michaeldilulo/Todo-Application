<template>
  <div class="todo-component">
    <div class="container-fluid">
      <div class="row">
        <div class="col-md-5">
          <p class="mt-3">
            If you click on the todo, it will put a line through it
          </p>
        </div>
      </div>
    </div>
    <div class="container-fluid">
      <div class="row">
        <div class="col-md-2 mt-5">
          <form @submit.prevent="createTodo" class="bg-dark pl-3">
            <label for="todo" class="mt-3 text-light">Enter Todo Here:</label>
            <br />
            <input
              type="text"
              name="newTodo"
              placeholder="Enter Todo Here..."
              v-model="newTodo"
            />
            <br />
            <button class="btn btn-success btn-sm mt-2 mb-3" type="submit">
              Submit Todo
            </button>
          </form>
        </div>
      </div>
    </div>
    <div class="container-fluid mt-5">
      <div class="row">
        <div class="col-md-3">
          <div class="row">
            <div class="col-md-12">
              <h2 class="d-flex justify-content-center">Todos Left:</h2>
            </div>
          </div>
          <ul class="bg-dark text-light">
            <li v-for="(todo, index) in todos" :key="todo.id">
              <div class="d-flex justify-content-between bg-dark">
                <h4
                  @click="toggleDone(todo)"
                  :class="{ done: todo.done }"
                  class="todo text-light d-flex"
                >
                  {{ todo.content }}
                </h4>
                <button
                  class="btn btn-danger btn-sm mt-3 mb-3 mr-3"
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
  align-items: center;
}
form {
  border-radius: 5px;
}
</style>