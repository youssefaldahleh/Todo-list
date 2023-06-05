<template>
  <the-header title="TRAKK 'EM ALL"></the-header>
  <todo-list></todo-list>
</template>
<script>
import TheHeader from "./components/Layouts/TheHeader.vue";
import TodoList from "./components/Todolist/TodoList.vue";
export default {
  components: {
    TheHeader,
    TodoList,
  },

};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background-color: rgb(23, 151, 236);
}
</style>
