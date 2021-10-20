<template>
  <div>
    <UserDisplay></UserDisplay>
    <H1>Todo User Add</H1>

    <form @submit.prevent="addUser">
      First Name:
      <input v-model="user.firstName" type="text" id="firstName">
      <br><br>
      Last Name:
      <input v-model="user.lastName" type="text" id="lastName">
      <br><br>
      Username:
      <input v-model="user.username" type="text" id="username">
      <br><br>
      Password:
      <input v-model="user.password" type="text" id="password">
      <br><br>
      <input type="submit" name="submit" value="Save">
      <button name="cancel" v-on:click.prevent="cancel()">Cancel</button>
    </form>
  </div>
</template>

<script>
import TodoServices from "@/services/TodoServices.js";
import UserDisplay from "@/components/UserDisplay.vue";
export default {
  components: {
    UserDisplay
  },
  data() {
    return {
      user: {}
    }
  },

  methods: {
    addUser() {
      TodoServices.addUser(this.user)
        .then(() => {
          this.$router.push({ name: 'list' })
        })
        .catch(error => {
          console.log(error);
        });
    },
    cancel() {
      this.$router.push({ name: 'list' })
    }
  }
}
</script>

<style>
</style>
