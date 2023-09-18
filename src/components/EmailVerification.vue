<template>
  <div>
    <h2>Email Verification</h2>
    <form @submit.prevent="verifyEmail">
      <div>
        <label for="userId">User ID:</label>
        <input type="text" id="userId" v-model="userId" required />
      </div>
      <div>
        <label for="token">Verification Token:</label>
        <input type="text" id="token" v-model="verificationToken" required />
      </div>
      <button type="submit">Verify Email</button>
    </form>
    <div v-if="verificationMessage">{{ verificationMessage }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userId: "", // Initialize userId as an empty string
      verificationToken: "",
      verificationMessage: ""
    };
  },
  methods: {
    async verifyEmail() {
      try {
        const response = await fetch(`http://localhost:7799/api/users/${this.userId}/verify-email`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({ token: this.verificationToken })
        });
        if (response.ok) {
          this.verificationMessage = "Email verified successfully!";
          // Perform any additional actions or navigation
        } else {
          const data = await response.json();
          this.verificationMessage = data.message; // Display any error message from the server
        }
      } catch (error) {
        console.error("Error during email verification:", error);
        this.verificationMessage = "An error occurred during email verification.";
      }
    }
  }
};
</script>

<style scoped>
/* Add any styles specific to this component here */
</style>
