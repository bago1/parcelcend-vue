<template>
  <div>
    <h2>Get Requests to Traveller's Listing</h2>
    <form @submit.prevent="getListingToTravellerListingId">
      <div>
        <label for="travellerListingId">Traveller Listing ID:</label>
        <input type="text" id="travellerListingId" v-model="travellerListingId" required />
      </div>
      <button type="submit">Get Listing</button>
    </form>

    <table v-if="listing" class="bordered-table">
      <thead>
        <tr>
          <th>Request ID</th>
          <th>Request Type</th>
          <th>Requested By Listing ID</th>
          <th>Requested To Listing ID</th>
          <th>Request Status</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="request in listing?.requests" :key="request.id">
          <td>{{ request.id || 'N/A' }}</td>
          <td>{{ request.requestType || 'N/A' }}</td>
          <td>{{ request.requestedByListingId || 'N/A' }}</td>
          <td>{{ request.requestedToListingId || 'N/A' }}</td>
          <td>{{ request.status || 'N/A' }}</td>
        </tr>
      </tbody>
    </table>

    <div v-else-if="error">
      <p>Error: {{ error }}</p>
    </div>
  </div>
</template>



<style scoped>
.bordered-table {
  border-collapse: collapse;
  width: 100%;
  border: 1px solid #ddd;
}

.bordered-table th, .bordered-table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

.bordered-table th {
  background-color: #f2f2f2;
}
</style>

<script>
export default {
  data() {
    return {
      travellerListingId: "",
      listing: null,
      error: null,
    };
  },
  methods: {
    async getListingToTravellerListingId() {
      try {
        const response = await fetch(
          `http://localhost:7799/api/requests/to-traveller-listing/${this.travellerListingId}`,
          {
            headers: {
              'accept': '*/*'
            }
          }
        );
        if (response.ok) {
          this.listing = await response.json();
          this.error = null;
        } else {
          const data = await response.json();
          this.error = data.message;
          this.listing = null;
        }
      } catch (error) {
        console.error("Error fetching listing:", error);
        this.error = "An error occurred while fetching the listing.";
        this.listing = null;
      }
    },
  },
};
</script>
