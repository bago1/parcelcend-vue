<template>
  <div>
    <h2>All Cities</h2>
    <table>
      <thead>
        <tr>
          <th>#  .</th>
          <th>City ID</th>
          <th>City Name</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(city, index) in cities" :key="city.id">
          <td>{{ index + 1 }}</td>
          <td>{{ city.cityId }}</td>
          <td>{{ city.cityName }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cities: [], // Initialize an empty array to store cities
    };
  },
  created() {
    // Fetch all cities from the Spring Boot API
    fetch('http://localhost:7799/api/locations/cities')
      .then((response) => response.json())
      .then((data) => {
        this.cities = data;
      })
      .catch((error) => {
        console.error('Error fetching cities:', error);
      });
  },
};
</script>
