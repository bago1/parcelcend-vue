<template>
  <div>
    <h1>Listings List</h1>
    <div>
      <button @click="getTravellerListings">TRAVELLER_LISTING</button>
      <button @click="getSenderListings">SENDER_LISTING</button>
    </div>
    <table>
      <thead>
        <tr>
          <th>Listing Id</th>
          <th>Departure Date</th>
          <th>Description</th>
          <th>CityName</th>
          <th>Type</th>
          <th>Fee</th>
          <!-- Add more table headers as needed -->
        </tr>
      </thead>
      <tbody>
        <tr v-for="listing in listings" :key="listing.id">
          <td>{{ listing.id }}</td>
          <td>{{ listing.departureDate }}</td>
          <td>{{ listing.description }}</td>
          <td>{{ listing.destination.cityName }}</td>
          <td>{{ listing.type }}</td>
          <td>{{ listing.fee }} AZN</td>
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
      listings: []
    };
  },
  async created() {
    // Fetch initial listings without a type parameter
    this.fetchListings();
  },
  methods: {
    async fetchListings(type = "") {
      try {
        // Create the URL based on the listing type
        const url = type
          ? `http://localhost:7799/api/listings?offset=0&pageSize=200&desc=false&sortBy=&type=${type}`
          : "http://localhost:7799/api/listings";

        const response = await fetch(url, {
          headers: {
            'accept': '*/*'
          }
        });
        this.listings = await response.json();
      } catch (error) {
        console.error("There was an error fetching the listings:", error);
      }
    },
    getTravellerListings() {
      this.fetchListings("TRAVELLER_LISTING");
    },
    getSenderListings() {
      this.fetchListings("SENDER_LISTING");
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
