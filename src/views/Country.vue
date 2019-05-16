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
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Country",
  data() {
    return {
      country: null
    };
  },
  mounted() {
    axios
      .get("/api/country/" + this.$route.params.countryName)
      .then(response => {
        this.country = response.data.country;
      })
      .catch(error => {
        console.error(error);
      });
  }
};
</script>
