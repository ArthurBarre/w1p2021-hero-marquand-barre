<template>
<body>
  <h1>{{game}}</h1>
  <h2> Il vous réstait {{foodQuantity}} Nourritures</h2>
  <h2>Il vous réstait {{waterQuantity}} Eau</h2>
  <router-link @click="reset" to="/game/Home">Rééssayer</router-link>
</body>
</template>

<script>
import healthService from '../services/healthService.js'
export default {
  data() {
    return {
      game: "Game Over",
      foodQuantity: healthService.foodValue(),
      waterQuantity: healthService.waterValue()
    };
  },methods: {
    reset(){
      
    }
  },
  mounted() {
  },
};
</script>
<style scoped>
* {
  font-family: "Neucha", cursive;
  color: var(--brand-color);
  letter-spacing: 2px;
}
body {
  width: 100vw;
  height: 100vh;
  background-image: url(../assets/img/Fonds/Loose.jpg);
  background-size: cover;
  background-repeat: no-repeat;
}
h1 {
  width: max-content;
  height: max-content;
  color: white;
  font-size: 200px;
  transform: translateY(350px);
  font-family: sans-serif;
  margin: auto auto;
}
h2{
  color : white;
  font-size: 50px;
  width: max-content;
  margin: 0 auto;
}
</style>

