<template>
  <div class="container">
    <h1>Welcom to Currency Converter Application</h1>
    <div class="container-items">
      <Currency/>
      <Converter/>
    </div>
  </div>
</template>

<script>
import Currency from './Currency.vue'
import Converter from './Converter.vue'
export default {
  components: { Currency, Converter },
  name: 'Container',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container{
  position: absolute;
  width: 90%;
  height: 80%;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
}

.container-items{
  display: flex;
  justify-content:space-evenly;
  align-items: center;
  height: 80%;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
