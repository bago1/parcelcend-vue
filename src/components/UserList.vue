<template>
  <div>
    <h1>User List</h1>
    <table>
      <thead>
        <tr>
          <th>User ID</th>
          <th>Name</th>
          <th>Email</th>
          <th>Phone</th>
          <th>Username</th>
          <th>Email Verified</th>
          <th>Phone Verified</th>
          <!-- Add more table headers as needed -->
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, index) in users" :key="user.id">
          <td>{{ index + 1 }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.phone }}</td>
          <td>{{ user.username }}</td>
          <td>{{ user.emailVerified ? 'Yes' : 'No' }}</td>
          <td>{{ user.phoneVerified ? 'Yes' : 'No' }}</td>
          <!-- Add more table data columns as needed -->
        </tr>
      </tbody>
    </table>
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
table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}
</style>
