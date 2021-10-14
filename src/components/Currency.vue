<template>
  <div class="currency">
    <div class="currency-item">
      <h2>Курс</h2> (Кыргызский сом)
    </div>
    <div class="currency-item">
      <img src="../assets/img/eu.svg" class="currency-icon" alt="KGS">
      <div class="currency-price">
        <p>Евро</p>
        <p>{{Math.round(this.euro*1000)/1000}}</p>
      </div>
    </div>
    <div class="currency-item">
      <img src="../assets/img/usd.svg" class="currency-icon" alt="KGS">
      <div class="currency-price">
        <p>Доллар</p>
        <p>{{Math.round(this.usd*1000)/1000}}</p>
      </div>
    </div>
    <div class="currency-item">
      <img src="../assets/img/try.svg" class="currency-icon" alt="KGS">
      <div class="currency-price">
        <p>Лира</p>
        <p>{{Math.round(this.try*1000)/1000}}</p>
      </div>
    </div>
    <div class="currency-item">
      <img src="../assets/img/rub.svg" class="currency-icon" alt="KGS">
      <div class="currency-price">
        <p>Рубль</p>
        <p>{{Math.round(this.rub*1000)/1000}}</p>
      </div>
    </div>
    <div class="currency-item">
      <img src="../assets/img/uzb.svg" class="currency-icon" alt="KGS">
      <div class="currency-price">
        <p>Сум</p>
        <p>{{Math.round(this.uzs*1000)/1000}}</p>
      </div>
    </div>
    <div class="currency-item">
      <img src="../assets/img/kgz.svg" class="currency-icon" alt="KGS">
      <div class="currency-price">
        <p>Тенге</p>
        <p>{{Math.round(this.kzt*1000)/1000}}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return{
      kgs: null,
      kzt: null,
      uzs: null,
      rub: null,
      baseCurrency: null,
      euro: null,
      try: null,
      usd: null
    }
  },
  methods: {
    getCurrency: async function(){
      const currency = await axios.get('http://data.fixer.io/api/latest?access_key=504ec486f332e8835e885163c0fd44f3')

      const base = currency.data.rates.EUR
      const baseCurrency = ((base / currency.data.rates.KGS) * 1)

      this.baseCurrency = baseCurrency

      this.euro = currency.data.rates.KGS
      this.usd = (base / currency.data.rates.USD) * currency.data.rates.KGS
      this.try = (base / currency.data.rates.TRY) * currency.data.rates.KGS
      this.rub = (base / currency.data.rates.RUB) * currency.data.rates.KGS
      this.uzs = (base / currency.data.rates.UZS) * currency.data.rates.KGS
      this.kzt = (base / currency.data.rates.KZT) * currency.data.rates.KGS

    }
  },
  created(){
    this.getCurrency()
  }
}
</script>

<style scoped>
.currency{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 20em;
  height: 25em;
  box-shadow: rgba(0, 0, 0, 0.25) 0px 0.0625em 0.0625em, rgba(0, 0, 0, 0.25) 0px 0.125em 0.5em, rgba(255, 255, 255, 0.1) 0px 0px 0px 1px inset;
  padding: 0 20px;
}
.currency-item{
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.currency-icon{
  width: 30px;
}

.currency-price{
  width: 80%;
  display: flex;
  justify-content: space-between;
}
</style>