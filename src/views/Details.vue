<template>
  <div class="">
    <table class="table table-bordered">
      <TableHead />
      <tbody>
        <TableRow
          description="Market Capitalization"
          :value="bitcoinData.marketcap"
        />
        <TableRow
          description="Total Bitcoins in circulation"
          :value="bitcoinData.totalbc"
        />
        <TableRow
          description="Number of transactions in the past 24 hours"
          :value="bitcoinData.transactionCount"
        />
        <TableRow
          description="Number of btc sent in the last 24 hours"
          :value="bitcoinData.btcSent"
        />
        <TableRow
          description="Estimated network hash rate in gigahash"
          :value="bitcoinData.hashRate"
        />
        <TableRow
          description="Current difficulty target as a decimal number"
          :value="bitcoinData.getDifficulty"
        />
      </tbody>
    </table>
  </div>
</template>

<script>
import TableHead from "../components/TableHead.vue";
import TableRow from "../components/TableRow.vue";
export default {
  components: { TableHead, TableRow },
  name: "Details",
  data() {
    return {
      bitcoinData: {
        marketcap: "",
        totalbc: "",
        transactionCount: "",
        btcSent: "",
        hashRate: "",
        getDifficulty: "",
      },
    };
  },
  methods: {
    async fetchBitcoinData() {
      Promise.all([
        fetch("https://blockchain.info/q/marketcap"),
        fetch("https://blockchain.info/q/totalbc"),
        fetch("https://blockchain.info/q/24hrbtcsent"),
        fetch("https://blockchain.info/q/24hrtransactioncount"),
        fetch("https://blockchain.info/q/hashrate"),
        fetch("https://blockchain.info/q/getdifficulty"),
      ]).then(async ([a, b, c, d, e, f]) => {
        const marketcap = await a.text();
        const bc = await b.text();
        const tc = await c.text();
        const btcent = await d.text();
        const hr = await e.text();
        const gd = await f.text();
        this.bitcoinData.marketcap = marketcap;
        this.bitcoinData.totalbc = bc;
        this.bitcoinData.transactionCount = tc;
        this.bitcoinData.btcSent = btcent;
        this.bitcoinData.hashRate = hr;
        this.bitcoinData.getDifficulty = gd;
      });
    },
  },
  created() {
    this.fetchBitcoinData();
  },

};
</script>
