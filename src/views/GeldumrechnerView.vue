
<template>
  <div id="app" class="geld-umrechner">
    <img alt="Vue logo" src="../assets/logo.png" />
    <h1>Timm's Währungsrechner</h1>
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
        `https://v6.exchangerate-api.com/v6/c8987c9a76b6c33d7c7d3c89/latest/${
          this.currency_one
        }`
      )
        .then((res) => res.json())
        .then((data) => {
          this.data = data;
          this.rate = data.conversion_rates[this.currency_two];
          this.amountTwo = this.amountOne * this.rate.toFixed(2);
          this.loggingResults()
        });
    },

    loggingResults() {
    if (this.amountOne && this.amountTwo != 0) {
      const inputObject = {
      currency: this.currency_one,
      input: this.amountOne,
      }
      const outputObject = {
      currency: this.currency_two,
      output: this.amountTwo,
      }
      console.log(inputObject, outputObject);
      // const fes = require('fs-extra');
      // fs.writeJson('./log.json', inputObject, (error) =>{
      // if (error) throw error
      // })
    }
    else{
      console.log("No Input");
    }
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
}

</script>

<style lang="sass">
html 
  background: #f4f4f4

#app 
  display: flex
  flex-direction: column
  align-content: center
  align-items: center
  /* justify-content: center; */
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif
  width: 100%
  height: 100%
  /* background: #f4f4f4f4; */
  /* border:1px solid red */

h1 
  color: #fb4c4c
  font-weight: 900

img 
  width: 150px

  &.hover
   animation: animation-in 500ms forwards

   @keyframes animation-in

    0%
        transform: translate(0, 0)
    50%
        transform: translate(0, 1rem)
    100%
        transform: translate(0, 1rem) rotate(5deg)
    @keyframes animation-out

    0%
         100%
         transform: translate(0, 1rem) rotate(5deg)
    50%
         transform: translate(0, 1rem)
    100%
         transform: translate(0, 0)

.container 
  width: 50%
  height: 100%
  display: flex
  flex-direction: column
  align-items: center
  justify-content: center
  text-align: center

.container-two 
  display: flex
  /* border: 1px solid black; */
  align-content: center
  align-items: center
  justify-content: center
  width: 50%
  justify-content: space-evenly


.container-two button 
  padding: 5px 
  font-size: 18px
  background: #fb4c4c
  color: #fff
  width: 30%
  height: 10%
  border: none
  outline: none
  cursor: pointer

  
select 
  padding: 5px
  /* width: 30%; */
  margin: 5px
  border: 1px solid rgba(0, 0, 0, 0.5)
  outline: none

input 
  padding: 5px
  font-size: 18px
  border: 1px solid rgba(0, 0, 0, 0.5)
  outline: none

#lastlyUpdated
  font-weight: 500

#baseValue 
  font-weight: 500

</style>
