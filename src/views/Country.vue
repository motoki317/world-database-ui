<template>
  <div>
    <div v-if="country">
      <h2>{{ country.name }} [ {{ country.code }} ]</h2>
      <p>
        地域: {{ country.region }}
        <br />
        面積: {{ country.surface_area }} km^2
        <br />
        人口: {{ country.population }} 人
        <br />
        平均寿命: {{ country.life_expectancy }} 年
        <br />
      </p>
    </div>
    <div v-else>Country not found...</div>
    <p>
      <router-link to="/countries">Back to countries list</router-link>
    </p>
    <div>
      <h3>{{ country.name }}の街</h3>
      <div class="cities-container">
        <div v-for="city in cities" :key="city.name">
          <div class="city">
            <router-link :to="'/city/' + city.name">{{
              city.name
            }}</router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Country",
  data() {
    return {
      country: null,
      cities: null
    };
  },
  mounted() {
    axios
      .get(
        "http://150.95.157.67:10901/country/" + this.$route.params.countryName
      )
      .then(response => {
        this.country = response.data.country;
      })
      .catch(error => {
        console.error(error);
      });
    axios
      .get(
        "http://150.95.157.67:10901/citiesInCountry/" +
          this.$route.params.countryName
      )
      .then(response => {
        this.cities = response.data.cities;
      })
      .catch(error => {
        console.error(error);
      });
  }
};
</script>
