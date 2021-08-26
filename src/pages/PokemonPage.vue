
<template>

  <h1 v-if="!pokemon">Cargando Pokemon...</h1>

  <div v-else>

    <h1>¿Quien es este pokemon?</h1>

    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon"/>
    <PokemonOptions @selection="checkAnswer($event)" :pokemonsOptions="pokemonsArray"/>

    <template v-if="showAnswer"> <!-- Remplaza un div para que no aparezca en el html -->

      <h2 class="fade-in">{{ message }}</h2>

      <button @click="newGame">Nuevo juego</button>

    </template>

  </div>

  
</template>

<script>

import PokemonPicture from '@/components/PokemonPicture.vue'
import PokemonOptions from '@/components/PokemonOptions.vue'

import getPokemonOptions from "@/helpers/getPokemonOptions"


export default {

  name: "PokemonPage",
  components: {
    PokemonPicture,
    PokemonOptions
  },
  data(){
    return {
      pokemonsArray: [],
      pokemon: null,
      showPokemon: false,
      showAnwer: false,
      message: ""
    }
  },
  methods: {

    async mixPokemonArray(){

      this.pokemonsArray = await getPokemonOptions()

      const randomInt = Math.floor(Math.random() * 4)

      this.pokemon = this.pokemonsArray[randomInt]

    },

    checkAnswer(pokemonId) {

      this.showPokemon = true
      this.showAnswer = true

      if(this.pokemon.id == pokemonId){
        this.message = `Correcto! Es ${this.pokemon.name}`
      }
      else {
        this.message = `Incorrecto! Era ${this.pokemon.name}`
      }

    },
    newGame(){
      this.showPokemon = false
      this.showAnswer = false
      this.pokemonsArray = []
      this.pokemon = null
      this.mixPokemonArray()
    }

  },
  mounted() {
    this.mixPokemonArray()
  }

}

</script>

<style scoped>

  button {
    background-color: rgb(69, 122, 238);
    border: none;
    border-radius: 5px;
    padding: 10px 30px;
    color: white;
  }

</style>
