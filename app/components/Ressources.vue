<template>
<transition name="fade">
  <div class="game__container">
    <div class="aside">
      <img class="logo" src="../assets/img/assets-components/LogoBig.png" alt="Logo">
      <img
        class="sound"
        src="../assets/img/assets-components/soundOff.png"
        alt="Turn the sound off"
      >
    </div>

    <div class="game__main">
      <h1>Jour {{day}}</h1>
      <div class="content__scale">
        <div class="ressources">
          <div class="ressource food">
            <Foods/>
          </div>
          <div class="ressource water">
            <Waters/>
          </div>
        </div>

        <div class="buttons">
          <div class="quantities foodQuantity">
            <p class="quantity">{{foodQuantity}}</p>
          </div>
          <div class="button button--food" @click="eat">
            <ItemFood/>
            <!-- <p>{{foodQuantity}}</p> -->
          </div>
          <div class="quantities waterQuantity">
            <p class="quantity">{{waterQuantity}}</p>
          </div>
          <div class="button button--water" @click="drink">
            <ItemWater/>
            <!-- <p>{{waterQuantity}}</p> -->
          </div>
        </div>
      </div>
      <div class="directions">
        <router-link class="direction direction--next" to="/game/Expeditions"></router-link>
      </div>
    </div>
    <aside>Une collaboration d'Arthur Barré & Kalani Marquand</aside>
  </div>
  </transition>
</template>

<style  lang="scss" scoped>
.content__scale {
  transform : scale(1.35) translateX(50px) translateY(50px)

}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
* {
  font-family: "Neucha", cursive;
  color: var(--brand-color);
  letter-spacing: 2px;
}
h1 {
  font-size: 90px;
  margin: 10% 0 2% 0;
  text-align: center;
}
.game__container {
  display: flex;
  width: 100vw;
  height: 100vh;
  background-image: url(../assets/img/Fonds/Game.jpg);
  background-repeat: no-repeat;
  background-size: cover;
  justify-content: center;
  align-items: center;
}
.game__main {
  margin: auto auto;
  width: 710px;
  height: 710px;
  margin-top: 4%;
  display: flex;
  align-items: center;
  flex-direction: column;
  background-image: url(../assets/img/assets-components/PaperFond.png);
}
.buttons {
  position: relative;
  display: flex;
  padding-top: 5%;
  width: 400px;
  justify-content: space-evenly;
}
.quantities {
  position: absolute;
  text-align: center;
  border-radius: 50%;
  background-color: white;
  width: 25px;
  height: 25px;
}
.quantity {
  font-size: 20px;
  margin-top: 20%;
}
.foodQuantity {
  left: 10%;
}
.waterQuantity {
  left: 55%;
}

.direction--next::after {
  position: absolute;
  right: 25%;
  bottom: 5%;
  content: url(../assets/img/assets-components/ArrowRight.png);
}

.aside {
  position: absolute;
  right: 15%;
  top: 8%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.logo {
  width: 150px;
}
.sound {
  width: 50px;
  margin-top: 20%;
}
aside {
  position: absolute;
  bottom: 5px;
  right: 5px;
  font-size: 16px;
}
</style>

<script>
import Foods from "./Foods.vue";
import Waters from "./Waters.vue";
import ItemFood from "../items/ItemFood.vue";
import ItemWater from "../items/ItemWater.vue";
import healthService from "../services/healthService";
import dayService from "../services/dayService";
import user from "../json/user.json";

export default {
  data: function() {
    return {
      day: null,
      waterQuantity: null,
      foodQuantity: null,
      thirst :null,
      hunger : null,
    };
  },
  components: {
    Foods,
    Waters,
    ItemWater,
    ItemFood
  },
  methods: {
    drink: function() {
      healthService.drink();
      this.waterQuantity = healthService.waterValue();
      this.thirst = healthService.thirstValue();
    },
    eat: function() {
      healthService.eat();
      this.foodQuantity = healthService.foodValue();
      this.hunger = healthService.hungerValue();

    }
  },
  mounted() {
    this.foodQuantity = healthService.foodValue();
    this.waterQuantity = healthService.waterValue();
    this.thirst = healthService.thirstValue();
    this.hunger = healthService.hungerValue();
    healthService.foodValue();
    this.day = dayService.test();
  }
};
</script>