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
            />
            <button class="btn btn-success" type="submit">Submit Todo</button>
          </form>
        </div>
      </div>
    </div>
    <div class="container-fluid">
      <div class="row">
        <div class="col-md-6"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "todo-component",
  setup() {
    function createTodo() {
      console.log("Todo was created");
    }
    return {
      createTodo,
    };
  },
};
</script>

<style>
</style>