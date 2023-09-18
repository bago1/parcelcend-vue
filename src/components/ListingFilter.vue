<template>
  <div>
    <h1>Listings List</h1>
    <ul>
      <li v-for="listing in listings" :key="listing.id">
        <div>
          <strong>Listing ID:</strong> {{ listing.id }}
        </div>
        <div>
          <strong>User ID:</strong> {{ listing.userId }}
        </div>
        <div>
          <strong>Origin:</strong> {{ listing.origin.city }} <!-- Assuming 'origin' has a 'city' property -->
        </div>
        <div>
          <strong>Destination:</strong> {{ listing.destination.city }} <!-- Assuming 'destination' has a 'city' property -->
        </div>
        <div>
          <strong>Description:</strong> {{ listing.description }}
        </div>
        <div>
          <strong>Departure Date:</strong> {{ listing.departureDate }}
        </div>
        <div>
          <strong>Arrival Date:</strong> {{ listing.arrivalDate }}
        </div>
        <div>
          <strong>Show All:</strong> {{ listing.showAll ? 'Yes' : 'No' }}
        </div>
        <div>
          <strong>Status:</strong> {{ listing.status }}
        </div>
        <div>
          <strong>Type:</strong> {{ listing.type }}
        </div>
        <div>
          <strong>Fee:</strong> {{ listing.fee }}
        </div>
        <!-- Add more fields as needed -->
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      listings: []
    };
  },
  async created() {
    try {
      const response = await fetch('http://localhost:7799/api/listings', {
        headers: {
          'accept': '*/*'
        }
      });
      this.listings = await response.json();
    } catch (error) {
      console.error("There was an error fetching the listings:", error);
    }
  }
};
</script>

<style scoped>
/* Add any styles specific to this component here */
</style>
