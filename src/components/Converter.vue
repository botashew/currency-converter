<template>
  <div class="converter">
      <h2>Калькулятор</h2>
      <div class="currency-value">
          <select name="currency-select" v-model="valueFrom" @change="this.convertCurrency">
              <option value="EUR">Евро</option>
              <option value="USD">Доллар</option>
              <option value="TRY">Лира</option>
              <option value="KGS">Сом</option>
              <option value="KZT">Тенге</option>
              <option value="UZS">Сум</option>
          </select>
          <input type="number" v-model="currencyFrom" @input="this.convertCurrency">
      </div>
      <div class="currency-value">
        <select name="currency-select" v-model="valueTo" @change="this.convertCurrency"> 
            <option value="EUR">Евро</option>
            <option value="USD">Доллар</option>
            <option value="TRY">Лира</option>
            <option value="KGS">Сом</option>
            <option value="KZT">Тенге</option>
            <option value="UZS">Сум</option>
        </select>
        <input type="number" v-model="currencyTo" @input="this.convertCurrencyBack">
      </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    data(){
        return{
            currencyFrom: '',
            currencyTo: '',
            currencies: {
                EUR: null,
                USD: null,
                TRY: null,
                RUB: null,
                KGS: null,
                KZT: null,
                UZS: null
            },
            valueFrom: 'EUR',
            valueTo: 'USD'
        }
    },
    methods: {
        getCurrency: async function(){
            const currency = await axios.get('https://currency-apit.herokuapp.com/rates')
            this.currencies.EUR = currency.data.rates.EUR
            this.currencies.USD = currency.data.rates.USD
            this.currencies.TRY = currency.data.rates.TRY
            this.currencies.RUB = currency.data.rates.RUB
            this.currencies.KGS = currency.data.rates.KGS
            this.currencies.KZT = currency.data.rates.KZT
            this.currencies.UZS = currency.data.rates.UZS
        },
        convertCurrency: function(){
            const base = this.currencies.EUR
            const data = ((base / this.currencies[this.valueFrom]) * this.currencies[this.valueTo]) * this.currencyFrom
            const roundData = Math.round(data * 100) / 100
            this.currencyTo = roundData

            if(this.currencyFrom===''){
                this.currencyTo = ''
            }
        },
        convertCurrencyBack: function(){
            const base = this.currencies.EUR
            const data = ((base / this.currencies[this.valueTo]) * this.currencies[this.valueFrom]) * this.currencyTo
            const roundData = Math.round(data * 100) / 100
            this.currencyFrom = roundData

            if(this.currencyTo===''){
                this.currencyFrom = ''
            }
        }
        
    }, 
    created(){
        this.getCurrency()
    }
}
</script>

<style>
.converter{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 30em;
  height: 20em;
  box-shadow: rgba(0, 0, 0, 0.25) 0px 0.0625em 0.0625em, rgba(0, 0, 0, 0.25) 0px 0.125em 0.5em, rgba(255, 255, 255, 0.1) 0px 0px 0px 1px inset;
  padding: 0 20px;
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button{
    -webkit-appearance: none;
    margin: 0;
}
input,
select{
    font-size: 16px;
    line-height: 28px;
    padding: 8px 16px;
    width: 50%;
    min-height: 44px;
    border: unset;
    border-radius: 4px;
    outline-color: rgb(84 105 212 / 0.5);
    background-color: rgb(255, 255, 255);
    box-shadow: rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(60, 66, 87, 0.16) 0px 0px 0px 1px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px;
}
select{
    width: 40%;
}
.currency-value{
    display: flex;
    justify-content: space-between;
    /* align-items: center; */
    width: 100%;
    margin: 5px 0;
}
.curreny-value > * {
    margin-right: 10px;
}
</style>