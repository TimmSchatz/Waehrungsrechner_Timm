
<template>
  <div id="app" class="geld-umrechner">
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>VueJs Currency Exchange App</h1>
    <div class="container">
      <div class="container-one">
        <select
          name="first-currency"
          id="first-currency"
          @change="calculateResults()"
          v-model="currency_one"
        >
          <option value="AED">AED</option>
          <option value="ARS">ARS</option>
          <option value="AUD">AUD</option>
          <option value="BGN">BGN</option>
          <option value="BRL">BRL</option>
          <option value="BSD">BSD</option>
          <option value="CAD">CAD</option>
          <option value="CHF">CHF</option>
          <option value="CLP">CLP</option>
          <option value="CNY">CNY</option>
          <option value="COP">COP</option>
          <option value="CZK">CZK</option>
          <option value="DKK">DKK</option>
          <option value="DOP">DOP</option>
          <option value="EGP">EGP</option>
          <option value="EUR">EUR</option>
          <option value="FJD">FJD</option>
          <option value="GBP">GBP</option>
          <option value="GTQ">GTQ</option>
          <option value="HKD">HKD</option>
          <option value="HRK">HRK</option>
          <option value="HUF">HUF</option>
          <option value="IDR">IDR</option>
          <option value="ILS">ILS</option>
          <option value="INR">INR</option>
          <option value="ISK">ISK</option>
          <option value="JPY">JPY</option>
          <option value="KRW">KRW</option>
          <option value="KZT">KZT</option>
          <option value="MXN">MXN</option>
          <option value="MYR">MYR</option>
          <option value="NOK">NOK</option>
          <option value="NZD">NZD</option>
          <option value="PAB">PAB</option>
          <option value="PEN">PEN</option>
          <option value="PHP">PHP</option>
          <option value="PKR">PKR</option>
          <option value="PLN">PLN</option>
          <option value="PYG">PYG</option>
          <option value="RON">RON</option>
          <option value="RUB">RUB</option>
          <option value="SAR">SAR</option>
          <option value="SEK">SEK</option>
          <option value="SGD">SGD</option>
          <option value="THB">THB</option>
          <option value="TRY">TRY</option>
          <option value="TWD">TWD</option>
          <option value="UAH">UAH</option>
          <option value="USD">USD</option>
          <option value="UYU">UYU</option>
          <option value="VND">VND</option>
          <option value="ZAR">ZAR</option>
        </select>
        <input
          type="number"
          name="input-one"
          id="input-one"
          v-model="amountOne"
          @input="calculateResults()"
        />
      </div>
      <div class="container-two">
        <button @click="switchValues()">Switch</button>
        <h4 id="baseValue">1 {{ currency_one }} = {{ rate }} {{ currency_two }}</h4>
      </div>
      <div class="container-there">
        <select
          id="currency-two"
          @change="calculateResults()"
          v-model="currency_two"
        >
          <option value="AED">AED</option>
          <option value="ARS">ARS</option>
          <option value="AUD">AUD</option>
          <option value="BGN">BGN</option>
          <option value="BRL">BRL</option>
          <option value="BSD">BSD</option>
          <option value="CAD">CAD</option>
          <option value="CHF">CHF</option>
          <option value="CLP">CLP</option>
          <option value="CNY">CNY</option>
          <option value="COP">COP</option>
          <option value="CZK">CZK</option>
          <option value="DKK">DKK</option>
          <option value="DOP">DOP</option>
          <option value="EGP">EGP</option>
          <option value="EUR">EUR</option>
          <option value="FJD">FJD</option>
          <option value="GBP">GBP</option>
          <option value="GTQ">GTQ</option>
          <option value="HKD">HKD</option>
          <option value="HRK">HRK</option>
          <option value="HUF">HUF</option>
          <option value="IDR">IDR</option>
          <option value="ILS">ILS</option>
          <option value="INR">INR</option>
          <option value="ISK">ISK</option>
          <option value="JPY">JPY</option>
          <option value="KRW">KRW</option>
          <option value="KZT">KZT</option>
          <option value="MXN">MXN</option>
          <option value="MYR">MYR</option>
          <option value="NOK">NOK</option>
          <option value="NZD">NZD</option>
          <option value="PAB">PAB</option>
          <option value="PEN">PEN</option>
          <option value="PHP">PHP</option>
          <option value="PKR">PKR</option>
          <option value="PLN">PLN</option>
          <option value="PYG">PYG</option>
          <option value="RON">RON</option>
          <option value="RUB">RUB</option>
          <option value="SAR">SAR</option>
          <option value="SEK">SEK</option>
          <option value="SGD">SGD</option>
          <option value="THB">THB</option>
          <option value="TRY">TRY</option>
          <option value="TWD">TWD</option>
          <option value="UAH">UAH</option>
          <option value="USD">USD</option>
          <option value="UYU">UYU</option>
          <option value="VND">VND</option>
          <option value="ZAR">ZAR</option>
        </select>

        <input
          type="number"
          id="amount-two"
          placeholder="0"
          v-model="amountTwo"
          disabled
        />
      </div>
      <div class="container-four">
        <h4 id="lastlyUpdated">Lastly Updated: {{ data.time_last_update_utc }}</h4>
      </div>
    </div>
  </div>
</template>



<script>
export default {
  name: "geld-umrechner",
  components: {},
  data() {
    return {
      data: [],
      currency_one: "USD",
      currency_two: "EUR",
      rate: "",
      amountOne: 1,
      amountTwo: 0,
    };
  },
  methods: {
    calculateResults() {
      fetch(
        `https://v6.exchangerate-api.com/v6/${"9809b1cec3fb53ce2b3f3f6a"}/latest/${
          this.currency_one
        }`
      )
        .then((res) => res.json())
        .then((data) => {
          this.data = data;
          this.rate = data.conversion_rates[this.currency_two];
          this.amountTwo = this.amountOne * this.rate.toFixed(2);
        });
    },
    switchValues() {
      const temp = this.currency_one;
      this.currency_one = this.currency_two;
      this.currency_two = temp;
      this.calculateResults();
    },
  },
  mounted() {
    this.calculateResults();
  },
};
</script>

<style>
html {
  background: #f4f4f4;
}
#app {
  display: flex;
  flex-direction: column;
  align-content: center;
  align-items: center;
  /* justify-content: center; */
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  width: 100%;
  height: 100%;
  /* background: #f4f4f4f4; */
  /* border:1px solid red */
}
h1 {
  color: #5fbaa7;
  font-weight: 900;
}
img {
  width: 150px;
}
.container {
  width: 50%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}
.container-two {
  display: flex;
  /* border: 1px solid black; */
  align-content: center;
  align-items: center;
  justify-content: center;
  width: 50%;
  justify-content: space-evenly;
}
.container-two button {
  padding: 5px;
  font-size: 18px;
  background: #5fbaa7;
  color: #fff;
  width: 30%;
  height: 10%;
  border: none;
  outline: none;
}
select {
  padding: 5px;
  /* width: 30%; */
  margin: 5px;
  border: 1px solid rgba(0, 0, 0, 0.5);
  outline: none;
}
input {
  padding: 5px;
  font-size: 18px;
  border: 1px solid rgba(0, 0, 0, 0.5);
  outline: none;
}
#lastlyUpdated{
  font-weight: 500;
}
#baseValue {
  font-weight: 500;
}
</style>
