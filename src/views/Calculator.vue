<template>
  <div class="container">
    <h2 class="header-calculator">Convert currencies to Bitcoins</h2>
    <form class="btc-form" @submit.prevent="handleSubmit">
      <div class="form-container">
        <div class="form-group-select">
          <label for="currencies">Currency: </label>

          <select id="currency" v-model="selected">
            <option disabled value="">Please select one</option>
            <option>EUR</option>
            <option>USD</option>
            <option>AUD</option>
            <option>NZD</option>
            <option>GBP</option>
          </select>
        </div>
        <div class="form-group-input">
          <label for="amount">Value: </label>
          <input
            id="amount"
            min="1"
            type="number"
            placeholder="500"
            v-model="amount"
          />
        </div>
      </div>
      <div class="btn">
        <button class="btn-lg btn-block btn-primary">Convert</button>
      </div>
    </form>
    <div class="result" v-if="query !== ''">
      {{ query }} {{ currency }} is {{ convertedSum }} BTC
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      selected: "",
      amount: 500,
      convertedSum: "",
      query: "",
      currency: "",
    };
  },
  methods: {
    async handleSubmit() {
      this.query = this.amount;
      this.currency = this.selected;
      try {
        const response = await fetch(
          `https://blockchain.info/tobtc?currency=${this.currency}&value=${this.query}`
        );
        const sum = await response.json();
        this.convertedSum = sum;
      } catch (err) {
        this.sum = err;
      }
    },
  },
};
</script>

<style>
.btc-form {
  width: 90%;
  margin: auto;
  padding: 1.25em 0;
}

.form-container {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
}

.form-group-select {
  padding-right: 2.5em;
}

#currency,
#amount {
  margin-left: 1.25em;
}

.btn {
  width: 100%;
}

.result {
  width: 70%;
  margin: auto;
  text-align: center;
}

button {
  background-color: blue;
  color: white;
  cursor: pointer;
  outline: none;
}

.header-calculator {
  margin-top: 2.5em;
  text-align: center;
}

.form-group-select,
.form-group-input {
  margin-bottom: 10px;
}
</style>
