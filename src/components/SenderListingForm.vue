<template>
  <div>
    <h2>Create Sender Listing</h2>
    <form @submit.prevent="createSenderListing">
      <div>
        <label for="departureDate">Departure Date:</label>
        <input type="datetime-local" id="departureDate" v-model="formData.departureDate" required />
      </div>
      <div>
        <label for="description">Description:</label>
        <input type="text" id="description" v-model="formData.description" required />
      </div>
      <div>
        <label for="originCityId">Origin City ID:</label>
        <input type="text" id="originCityId" v-model="formData.location.originCityId" required />
      </div>
      <div>
        <label for="destinationCityId">Destination City ID:</label>
        <input type="text" id="destinationCityId" v-model="formData.location.destinationCityId" required />
      </div>
      <div>
        <label for="fee">Fee:</label>
        <input type="number" id="fee" v-model="formData.fee" required />
      </div>
      <button type="submit">Create Listing</button>
    </form>
    <div v-if="responseMessage">{{ responseMessage }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        departureDate: "",
        description: "",
        location: {
          originCityId: "",
          destinationCityId: ""
        },
        fee: null
      },
      responseMessage: ""
    };
  },
  methods: {
    async createSenderListing() {
      try {
        const response = await fetch("http://localhost:7799/api/listings/sender", {
          method: "POST",
          headers: {
            "Content-Type": "application/json"
          },
          body: JSON.stringify(this.formData)
        });
        if (response.ok) {
          this.responseMessage = "Sender listing created successfully!";
          // Optionally, you can reset the form data here
          this.formData = {
            departureDate: "",
            description: "",
            location: {
              originCityId: "",
              destinationCityId: ""
            },
            fee: null
          };
        } else {
          const data = await response.json();
          this.responseMessage = data.message;
        }
      } catch (error) {
        console.error("Error creating sender listing:", error);
        this.responseMessage = "An error occurred while creating the listing.";
      }
    }
  }
};
</script>

<style scoped>
/* Add any styles specific to this component here */
</style>
