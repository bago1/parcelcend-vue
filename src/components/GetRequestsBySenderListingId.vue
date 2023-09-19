<template>
  <div>
    <h2>Get Requests to Sender's Listing</h2>
    <form @submit.prevent="getListingBySenderListingId">
      <div>
        <label for="senderListingId">Sender Listing ID:</label>
        <input type="text" id="senderListingId" v-model="senderListingId" required />
      </div>
      <button type="submit">Get Listing</button>
    </form>

    <table v-if="listing" class="bordered-table">
      <thead>
        <tr>
          <th>Listing ID</th>
          <th>User ID</th>
          <th>Origin City</th>
          <th>Destination City</th>
          <th>Description</th>
          <th>Departure Date</th>
          <th>Arrival Date</th>
          <th>Show All</th>
          <th>Status</th>
          <th>Type</th>
          <th>Fee</th>
          <th>Request ID</th>
          <th>Request Type</th>
          <th>Requested By Listing ID</th>
          <th>Request Status</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>{{ listing.id }}</td>
          <td>{{ listing.userId }}</td>
          <td>{{ listing.origin.cityName }}</td>
          <td>{{ listing.destination.cityName }}</td>
          <td>{{ listing.description }}</td>
          <td>{{ listing.departureDate }}</td>
          <td>{{ listing.arrivalDate }}</td>
          <td>{{ listing.showAll ? 'Yes' : 'No' }}</td>
          <td>{{ listing.status }}</td>
          <td>{{ listing.type }}</td>
          <td>{{ listing.fee }}</td>
          <td>{{ listing.requests[0].id }}</td>
          <td>{{ listing.requests[0].requestType }}</td>
          <td>{{ listing.requests[0].requestedByListingId }}</td>
          <td>{{ listing.requests[0].status }}</td>
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
      senderListingId: "",
      listing: null,
      error: null,
    };
  },
  methods: {
    async getListingBySenderListingId() {
      try {
        const response = await fetch(
          `http://localhost:7799/api/requests/to-sender-listing/${this.senderListingId}`,
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
