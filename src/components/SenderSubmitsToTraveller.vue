<template>
  <div>
    <h2>Sender Submits to Traveller</h2>
    <form @submit.prevent="submitRequest">
      <div>
        <label for="senderListingId">Sender Listing:</label>
        <select v-model="senderListingId" id="senderListingId">
          <option v-for="sender in senderListings" :key="sender.id" :value="sender.id">{{ sender.id }}</option>
        </select>
      </div>
      <div>
        <label for="travelerListingId">Traveler Listing:</label>
        <select v-model="travelerListingId" id="travelerListingId">
          <option v-for="traveler in travelerListings" :key="traveler.id" :value="traveler.id">{{ traveler.id }}</option>
        </select>
      </div>
      <div>
        <label for="action">Action:</label>
        <select v-model="action" id="action">
          <option value="SUBMIT">Submit</option>
          <option value="CANCEL">Cancel</option>
        </select>
      </div>
      <button type="submit">Submit Request</button>
    </form>
  </div>
</template>


<script>
export default {
  data() {
    return {
      senderListingId: "",
      travelerListingId: "",
      action: "SUBMIT", // Default action
      senderListings: [], // Initialize with an empty array
      travelerListings: [], // Initialize with an empty array
    };
  },
  created() {
    // Fetch sender listings and traveler listings from your API
    this.fetchSenderListings();
    this.fetchTravelerListings();
  },
  methods: {
    async fetchSenderListings() {
      try {
        const response = await fetch(`http://localhost:7799/api/listings?type=SENDER_LISTING`);
        if (response.ok) {
          this.senderListings = await response.json();
        } else {
          console.error("Error fetching sender listings");
        }
      } catch (error) {
        console.error("Error fetching sender listings:", error);
      }
    },
    async fetchTravelerListings() {
      try {
        const response = await fetch(`http://localhost:7799/api/listings?type=TRAVELLER_LISTING`);
        if (response.ok) {
          this.travelerListings = await response.json();
        } else {
          console.error("Error fetching traveler listings");
        }
      } catch (error) {
        console.error("Error fetching traveler listings:", error);
      }
    },
    async submitRequest() {
         // Construct the requestAction object
         const requestAction = {
           action: this.action,
           senderListingId: this.senderListingId,
           travelerListingId: this.travelerListingId,
         };

         try {
           const response = await fetch('http://localhost:7799/api/requests/submit-request/sender-to-traveler', {
             method: 'POST',
             headers: {
               'Content-Type': 'application/json',
             },
             body: JSON.stringify(requestAction),
           });

           if (response.ok) {
             // Request was successful, handle any success logic here
             console.log('Request submitted successfully');
           } else {
             // Request failed, handle error
             console.error('Error submitting request:', response.statusText);
           }
         } catch (error) {
           // Network or other errors
           console.error('Error submitting request:', error);
         }
       },
     },
   };
   </script>