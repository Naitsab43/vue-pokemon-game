
<template>
  
  <div class="options-container">

    <ul>

      <li 
        v-for="pokemon in capitalizePokemons" 
        :key="pokemon.id"
        @click="handleClickAnswer(pokemon)" >

        {{ pokemon.name }}

      </li>

    </ul>

  </div>

</template>

<script>

export default {

  props: {
    pokemonsOptions: {
      type: Array,
      required: true,
    }
  },
  name: "PokemonOptions",
  data(){
    return {
      answered: false
    }
  },
  computed: {

    capitalizePokemons(){
      
      for(let i in this.pokemonsOptions){
        
        this.pokemonsOptions[i].name = this.pokemonsOptions[i].name.charAt(0).toUpperCase() + this.pokemonsOptions[i].name.slice(1)

      }

      return this.pokemonsOptions;

    }

  },
  methods: {
    handleClickAnswer(pokemon){

      if(!this.answered){

        this.answered = true;
        this.$emit('selection', pokemon.id)

      }
      
    }
  }

}

</script>

<style scoped>

ul {
  list-style-type: none;
}

li {
  background-color: white;
  border-radius: 5px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid rgba(0, 0, 0, 0.2);
  cursor: pointer;
  margin-bottom: 10px;
  width: 250px;
}

li:hover {
  background-color: rgba(0, 0, 0, 0.05);
}

.options-container {
  display: flex;
  justify-content: center;
}

</style>