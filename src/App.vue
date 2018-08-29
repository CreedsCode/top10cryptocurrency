<template>
  <div  id="app">
    <h1>Top 10 Crypto Currencies</h1>
    <div id="crypto-container" v-for="(value,key) in cryptos">
      <span class="left">{{ key }}</span>
      <span class="right">{{ value.EUR }}€</span>
    </div>
    <p>Updated "28 August 2018"</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "app",
  data: () => ({
    cryptos: [],
    errors: []
  }),
  created() {
    axios
      .get(
        "https://min-api.cryptocompare.com/data/pricemulti?fsyms=BTC,ETH,EOS,BCH,XRP,ETC,DASH,NEO,IOTA&tsyms=EUR"
      )
      .then(response => {
        this.cryptos = response.data;
      })
      .catch(e => {
        this.errors.push(e);
      });
  }
};
</script>

<style>
p {
  text-align: center;
}
h1 {
  text-align: center;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
body {
  background: #f1f1f1;
}

div#crypto-container {
  background: white;
  width: 70%;
  margin: 0 auto 4px auto;
  padding: 1em;
  box-shadow: 1px 1px 0 lightgrey;
}

span.left {
  font-weight: bold;
}

span.right {
  float: right;
}
</style>