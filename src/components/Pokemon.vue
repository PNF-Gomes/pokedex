/* Pokemon card */

<template>
  <div>
    <!-- Card with showAbilites function that display other card when the mouse passes over -->
    <div
      class="md-elevation-1"
      v-if="showAbilities"
      id="pokeCard"
      @mouseover="showAbilitiesF()"
      
    >
    <!-- Pokemon name with filter -->
      <h1>{{ name | FirstLetterUpperCase }}</h1>
  <!-- pokemon front image -->
      <img :src="image_front" alt="" />
    </div>
    <!-- Here starts the card Extension display -->
    <div
      class="md-elevation-10"
      v-else
      id="pokeCardExtension"
      @mouseout="showAbilitiesF()"
    >
    <!-- name with filter -->
      <h1>{{ name | FirstLetterUpperCase }}</h1>
  <div class="container">
    <p></p>
    <p></p>
    <!-- pokemon front image -->
      <img  :src="image_front" alt="" />
      <div >
        <!-- pokemon skills from abilities array -->
        <h4>Skills:</h4>
      <p id="pSelect" v-for="(ability, index) in abilities" :key="index">
        {{ ability.ability.name }}
      </p>
      <p></p>
      </div>
      <!-- back image -->
        <img :src="image_back" alt="">
      </div>
      

     
    </div>
  </div>
</template>

<script>
/* Importing js library to make http requests */
import axios from "axios";

export default {
  /* using url passed by App.vue to make a API request */
  created: function () {
    axios.get(this.url).then((res) => {
      console.log(res.data.sprites.back_default),
        (this.abilities = res.data.abilities);
      this.image_front = res.data.sprites.front_default;
      this.image_back = res.data.sprites.back_default;
    });
  },
  props: {
    /* Values passed by App.vue */
    num: Number,
    name: String,
    url: String,
  },
  data: function () {
    return {
      /* Internal data */
      image_front: String,
      image_back:String,
      /* Abilities array */
      abilities: [],
      showAbilities: true,
    };
  },
  filters: {
    /* Filter for upperCasing first letter of the name */
    FirstLetterUpperCase: function (value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
  methods: {
    /* Switch between cards */
    showAbilitiesF() {
      this.showAbilities = !this.showAbilities;
    },
  },
};
</script>

<style scoped>
#pokeCard {
  text-align: center ;
  min-height: 20% ;
  max-width: 100% ;
  min-width: 25% ;
  margin-top: 10% ;
  margin: auto ;
  background: radial-gradient(
    circle,
    rgb(203, 255, 212) 0%,
    rgba(221, 232, 166, 0) 50%
  );
}
#pokeCardExtension {
  text-align: center ;
  min-height: 20% ;
  max-width: 200% ;
  min-width: 25% ;
  margin-top: 10% ;
  margin: auto ;

  background: radial-gradient(
    circle,
    rgb(176, 235, 196) 0%,
    rgba(221, 232, 166, 0) 80%
  );
  
}

.container{
  text-align: center;
  display: grid;
  grid-template-columns: repeat(7,1fr);

}




</style>