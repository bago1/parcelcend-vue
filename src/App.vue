<template>
  <div id="app">
    <UserList />
    <UserRegistration />
    <EmailVerification :userId="userId" />
    <Listings />
  </div>
</template>

<script>
import UserList from './components/UserList.vue';
import UserRegistration from './components/UserRegistration.vue';
import EmailVerification from './components/EmailVerification.vue';
import Listings from './components/ListingFilter.vue'; // Import the Listings component

export default {
  name: 'App',
  components: {
    UserList,
    UserRegistration,
    EmailVerification,
    Listings, // Include the Listings component
  },
  data() {
    return {
      userId: "your_actual_user_id_here", // Replace this with the actual user ID
    };
  },
};
</script>

<style>
/* Global styles */
</style>
