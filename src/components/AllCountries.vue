<template>
  <div>
    <h2>All Countries</h2>
    <table>
      <thead>
        <tr>
          <th>#  .</th>
          <th>Country ID</th>
          <th>Country Name</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(country, index) in countries" :key="country.id">
          <td>{{ index + 1 }}</td>
          <td>{{ country.countryId }}</td>
          <td>{{ country.countryName }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      countries: [], // Initialize an empty array to store countries
    };
  },
  created() {
    // Fetch all countries from the Spring Boot API
    fetch('http://localhost:7799/api/locations/countries')
      .then((response) => response.json())
      .then((data) => {
        this.countries = data;
      })
      .catch((error) => {
        console.error('Error fetching countries:', error);
      });
  },
};
</script>
