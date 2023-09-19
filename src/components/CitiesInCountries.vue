<template>
  <div>
    <h2>Cities in Country</h2>
    <select v-model="selectedCountry" @change="fetchCitiesInCountry">
      <option value="">Select a Country</option>
      <option v-for="country in countries" :key="country.countryId" :value="country.countryId">{{ country.countryName }}</option>
    </select>

    <table v-if="cities.length > 0">
      <thead>
        <tr>
          <th>ID</th>
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
      selectedCountry: '', // Initialize the selected country
      countries: [],       // Initialize an empty array to store countries
      cities: [],          // Initialize an empty array to store cities
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
  methods: {
    fetchCitiesInCountry() {
      if (this.selectedCountry) {
        // Fetch cities in the selected country from the Spring Boot API
        fetch(`http://localhost:7799/api/locations/cities/${this.selectedCountry}`)
          .then((response) => response.json())
          .then((data) => {
            this.cities = data;
          })
          .catch((error) => {
            console.error('Error fetching cities in country:', error);
          });
      } else {
        // Reset the cities when no country is selected
        this.cities = [];
      }
    },
  },
};
</script>
