<template>
  <div id="app">
    <UserList />
    <UserRegistration />
    <EmailVerification :userId="userId" />
    <hr> <!-- Horizontal line separator -->
    <AllCountries />
    <CitiesInCountries />
    <AllCities />
    <hr> <!-- Horizontal line separator -->
    <SenderListingForm />
    <TravellerListingForm />
    <hr> <!-- Horizontal line separator -->
    <Listings />
    <hr>
    <GetRequestsToSenderBySenderListingId />
      <hr>
    <GetRequestsToTravelListing />
    <SenderSubmitsToTraveller/>
  </div>
</template>


<script>
import UserList from './components/UserList.vue';
import UserRegistration from './components/UserRegistration.vue';
import EmailVerification from './components/EmailVerification.vue';
import Listings from './components/ListingFilter.vue';
import SenderListingForm from './components/SenderListingForm.vue';
import TravellerListingForm from './components/TravellerListingForm.vue';
import AllCities from './components/AllCities.vue';
import AllCountries from './components/AllCountries.vue';
import CitiesInCountries from './components/CitiesInCountries.vue';
import GetRequestsToSenderBySenderListingId from './components/GetRequestsBySenderListingId.vue';
import GetRequestsToTravelListing from './components/GetRequestsToTravelListing.vue';
import SenderSubmitsToTraveller from './components/SenderSubmitsToTraveller.vue';


export default {
  name: 'App',
  components: {
    UserList,
    UserRegistration,
    EmailVerification,
    Listings, // Include the Listings component,
    SenderListingForm,
    AllCities,
    AllCountries,
    CitiesInCountries,
    TravellerListingForm,
    GetRequestsToSenderBySenderListingId,
    GetRequestsToTravelListing,
    SenderSubmitsToTraveller
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
