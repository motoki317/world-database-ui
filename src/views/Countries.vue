<template>
  <div>
    <div class="country-container">
      <div v-for="country in countries" :key="country.name">
        <div class="country">
          <router-link :to="'/country/' + country.name">{{
            country.name
          }}</router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Countries",
  data() {
    return {
      countries: null
    };
  },
  mounted() {
    // ロード時に実行する関数
    axios
      .get("/api/countries")
      .then(res => {
        this.countries = res.data.countries;
      })
      .catch(error => {
        console.error(error);
      });
  }
};
</script>
