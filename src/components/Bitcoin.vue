<template>
  <div class="currency-box">
    <div
      class="currency-item"
      :key="index"
      v-for="(currency, index) in currencyData"
    >
      <h3>Currency: {{ currency.name }}</h3>
      <div :key="index" v-for="(data, index) in currency.data">
        <p>Purchase price: {{ data.buy }}</p>
        <p>Selling price: {{ data.sell }}</p>
        <div></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Bitcoin",
  props: {
    currencyData: Array,
  },
  data() {
    return {};
  },
  mounted() {

  },
};
</script>

<style scoped>
.currency-box {
  display: grid;
  align-items: center;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 2.3em;
  margin-top: 3.25em;
}

.currency-item {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 1.25em 0;
  border: 2px solid black;
  box-shadow: 0 2px 5px rgb(102, 97, 97);
}
</style>
