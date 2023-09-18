<template>
  <div>
    <h1>User List</h1>
    <ul>
      <li v-for="user in users" :key="user.id">{{ user.name }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: []
    };
  },
  async created() {
    try {
      const response = await fetch('http://localhost:7799/api/users', {
        headers: {
          'accept': '*/*'
        }
      });
      this.users = await response.json();
    } catch (error) {
      console.error("There was an error fetching the users:", error);
    }
  }
};
</script>

<style scoped>
/* Add any styles specific to this component here */
</style>
