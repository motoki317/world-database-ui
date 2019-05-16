<template>
  <div>
    <div v-if="cityInfo">
      <h2>{{ cityInfo.name }} [ {{ cityInfo.countryCode }} ]</h2>
      <p>人口: {{ cityInfo.population }}</p>
    </div>
    <div v-else>City not found...</div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "City",
  data() {
    return {
      cityInfo: null
    };
  },
  mounted() {
    const cityName = this.$route.params.cityName;
    axios.get("/api/city/" + cityName).then(response => {
      this.cityInfo = response.data.city;
    });
  }
};
</script>
