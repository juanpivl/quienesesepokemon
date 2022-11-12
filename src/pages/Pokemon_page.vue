<template   >
  <br />
  <br />
  <br />
  <br />

  <h1 v-if="!pokemon">Espere porfavor...</h1>

  <template v-else >
    <div class="columna">
      <h1>Intentos Correctos: {{ correcto }}</h1>
      <h1>Record: {{record}}</h1>
    </div>
    <div class="columna">
      <div>
        <h1>Quien es ese pokemon?</h1>
        <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
       <div v-if="!showAnswer">

         <PokemonOptions :pokemons="pokemonArr" @selection="checkAnswer" />
       </div>

        <br>
        <div v-if="showAnswer">
          <button @click="newgame">New game</button>
          
      </div>
        
        
      </div>
    </div>
    <div class="columna">
      <div v-if="showAnswer">
          <h2 class="fade-in">{{ message }}</h2>
          
      </div>
    </div>
  </template>
</template>

<script>
import PokemonOptions from "@/components/PokemonOptions.vue";
import PokemonPicture from "@/components/PokemonPicture.vue";

import getPokemonOptions from "@/helpers/getPokemonOptions";
 
export default {
  components: {
    PokemonOptions,
    PokemonPicture,
  },
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: "",
      correcto: 0,
      record: 0
    };
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonArr = await getPokemonOptions();

      const rndInt = Math.floor(Math.random() * 4);
      this.pokemon = this.pokemonArr[rndInt];

      //console.log(this.pokemon)

    },
    checkAnswer(selectedId) {
      this.showPokemon = true;
      this.showAnswer = true;
      if (selectedId === this.pokemon.id) {
        this.correcto = this.correcto + 1;
        this.record = this.correcto
        this.newgame();
      } else {
        this.message = `Uppss, era  ${this.pokemon.name}, vuelve a intentarlo`;
        this.correcto = 0;
      }
    },
    newgame() {
      this.showPokemon = false;
      this.showAnswer = false;
      this.pokemonArr = [];
      this.pokemon = null;
      this.mixPokemonArray();
    },
    
  },
  mounted() {
    this.mixPokemonArray();
  },
};
</script>


<style scoped>


.columna {
  float: left;
  width: 33%;
  border: 0px solid;
}
@media (max-width: 980px) {
  .columna {
    float: none;
    width: 100%;
  }
}
</style>



