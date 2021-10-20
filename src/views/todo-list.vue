<template>
  <div>
    <UserDisplay></UserDisplay>
    <H1>Todo List with Vue</H1>
    <TodoListDisplay v-for="todolist in todolists" :key="todolist.id" :todolist="todolist"/>
  </div>
</template>

<script>
import TodoListDisplay from "@/components/TodoListDisplay.vue";
import UserDisplay from "@/components/UserDisplay.vue";
import TodoServices from "@/services/TodoServices.js";
export default {
  components: {
    TodoListDisplay,
    UserDisplay
  },
  data() {
    return {
      todolists: []
    }
  },
  created() {
    TodoServices.getLists()
      .then(response => {
        this.todolists = response.data.lists;
      })
      .catch(error => {
        console.log('There was an error:', error.response)
      })
  }
}
</script>

<style></style>
