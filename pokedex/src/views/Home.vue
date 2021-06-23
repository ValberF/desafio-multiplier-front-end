<template>
  <div class="home">
    <h1>Pokémons</h1>
    <b-container>
      <b-row align-h="around">
        <Card
          v-for="(pokemon, index) in PokemonList"
          :key="index"
          :title="pokemon.name"
          :image="imgURL + (index + 1) + '.png'"
          :imgAlt="pokemon.name"
        />
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Card from "../components/Card.vue";

export default {
  name: "Home",
  components: { Card },
  data() {
    return {
      PokemonList: [],
      imgURL: "https://pokeres.bastionbot.org/images/pokemon/",
    };
  },
  methods: {
    getPokemons() {
      let Pokedex = require("pokedex-promise-v2");
      let P = new Pokedex();
      let interval = this.pokemonInterval();

      P.getPokemonsList(interval).then((res) => {
        this.PokemonList = res.results;
      });

      //alert(JSON.stringify(response))
    },
    pokemonInterval() {
      let interval = {
        limit: 151,
        offset: 0,
      };

      return interval;
    },
  },
  mounted() {
    this.getPokemons();
  },
};
</script>

<style scoped>
.home {
  display: flex;
  align-items: center;
  flex-direction: column;
}

h1 {
  margin-bottom: 30px;
}
</style>
