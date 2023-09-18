<template>
  <div>
    <h2>User Registration</h2>
    <form @submit.prevent="registerUser">
      <div>
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="user.name" required />
      </div>
      <div>
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="user.email" required />
      </div>
      <div>
        <label for="phone">Phone:</label>
        <input type="tel" id="phone" v-model="user.phone" required />
      </div>
      <div>
        <label for="username">Username:</label>
        <input type="text" id="username" v-model="user.username" required />
      </div>
      <div>
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="user.password" required />
      </div>
      <button type="submit">Register</button>
    </form>
    <div v-if="registrationMessage">{{ registrationMessage }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: {
        name: generateRandomName(),
        email: generateRandomEmail(),
        phone: generateRandomPhone(),
        username: generateRandomUsername(),
        password: generateRandomPassword()
      },
      registrationMessage: ""
    };
  },
  methods: {
    async registerUser() {
      try {
        const response = await fetch('http://localhost:7799/api/users/register', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(this.user)
        });
        if (response.ok) {
          this.registrationMessage = "Registration successful!";
          // Clear form or redirect to another page as needed
        } else {
          const data = await response.json();
          this.registrationMessage = data.message; // Display any error message from the server
        }
      } catch (error) {
        console.error("Error during registration:", error);
        this.registrationMessage = "An error occurred during registration.";
      }
    }
  }
};

function generateRandomName() {
  // Generate a random name as needed
  return "Random Name";
}

function generateRandomEmail() {
  // Generate a random email with a unique component
  return `user_${Date.now()}@example.com`;
}

function generateRandomPhone() {
  // Generate a random phone number as needed
  return "123-456-7890";
}

function generateRandomUsername() {
  // Generate a random username with a unique component
  return `user_${Date.now()}`;
}

function generateRandomPassword() {
  // Generate a random password as needed
  return "RandomPassword";
}
</script>

<style scoped>
/* Add any styles specific to this component here */
</style>
