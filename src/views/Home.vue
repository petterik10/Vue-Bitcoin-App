<template>
  <div>
    <div class="container">
      <h1 class="main-header">Bitcoin prices in different currencies</h1>
      <div class="">
        <Bitcoin :currencyData="currencyData" />
      </div>
    </div>
  </div>
</template>

<script>
import Bitcoin from "../components/Bitcoin.vue";

export default {
  components: { Bitcoin },
  name: "Home",
  data() {
    return {
      currencyData: [],
    };
  },
  methods: {
    async fetchBitcoins() {
      try {
        const response = await fetch("https://blockchain.info/ticker");
        const json = await response.json();
        const objArray = Object.entries(json).map((elem) => {
          return { name: elem[0], data: [elem[1]] };
        });
        return objArray;
      } catch (err) {
        console.log(err);
      }
    },
  },
  async created() {
    this.currencyData = await this.fetchBitcoins();
  },
};
</script>

<style scoped>
.card-grid {
  display: grid;
  align-items: center;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 2.3em;
  margin-top: 3.25em;
}

.main-header {
  text-align: center;
  margin: 0.5em;
}
</style>
