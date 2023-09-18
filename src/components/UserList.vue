<template>
  <div>
    <h1>User List</h1>
    <ul>
      <li v-for="user in users" :key="user.id">
       <div>
           <strong>User ID:</strong> {{ user.id }}
        </div>
        <div>
          <strong>Name:</strong> {{ user.name }}
        </div>
        <div>
          <strong>Email:</strong> {{ user.email }}
        </div>
        <div>
          <strong>Phone:</strong> {{ user.phone }}
        </div>
        <div>
          <strong>Username:</strong> {{ user.username }}
        </div>
        <div>
          <strong>Email Verified:</strong> {{ user.emailVerified ? 'Yes' : 'No' }}
        </div>
        <div>
          <strong>Phone Verified:</strong> {{ user.phoneVerified ? 'Yes' : 'No' }}
        </div>
        <!-- Add more details as needed -->
      </li>
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
