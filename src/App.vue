<template>
  <todoHeader />
  <todoComponent />
</template>

<script>
import todoHeader from "@/components/TodoHeader";
import todoComponent from "@/components/TodoComponent";

export default {
  name: "App",
  components: {
    todoHeader,
    todoComponent,
  },
};
</script>

<style>
</style>
