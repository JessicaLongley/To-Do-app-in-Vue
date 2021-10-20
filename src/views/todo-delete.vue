<template>
  <div>
    <H1>Todo List Delete</H1>
    <h4>Delete {{ list.name }} ?</h4>
    <button v-on:click="deleteTodoList()">Delete</button>
    <button v-on:click="cancel()">Cancel</button>
  </div>
</template>

<script>
import TodoServices from "@/services/TodoServices.js";
export default {
  props: ["id"],

  data() {
    return {
      list: Object
    };
  },
  created() {
    TodoServices.getList(this.id) //use the id that was passed in
        .then(response => {
        this.list = response.data.list;
      })
      .catch(error => {
        console.log('There was an error:', error.response)
      })
  },

  methods: {
    deleteTodoList() {
      TodoServices.deleteList(this.id)
        .then(response => {
          this.$router.push({ name: "list" })
          console.log(response)
        })
        .catch(error => {
          console.log(error.data)
        })
    },
    cancel() {
      this.$router.push({ name: "list" })
    }
  }
}
</script>

<style></style>
