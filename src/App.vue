<template>
  <div id="app">
    <h1>Bitcoin Price Index</h1>
    <div v-for="currency in info" v-bind:key="currency">>
      {{ currency.description }}:
      <span class="lighten">
        <span v-html="currency.symbol"></span
        >{{ currency.rate_float | currencydecimal }}
      </span>
    </div>
  </div>
</template>
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vue@2"></script>

<script>
import axios from "axios";

export default {
  name: "app",
  data() {
    return {
      info: null,
    };
  },
  async created() {
    try {
      const res = await axios.get(
        `https://api.coindesk.com/v1/bpi/currentprice.json`
      );

      this.info = res.data.bpi;
    } catch (e) {
      console.error(e);
    }
  },
};
</script>

<style></style>
