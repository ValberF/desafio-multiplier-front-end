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
        >
          <b-button
            @click="getPokemonData(index + 1, pokemon.name, pokemon.url)"
            variant="primary"
            >Capturar</b-button
          >
        </Card>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Card from "../components/Card.vue";
import axios from "axios";

export default {
  name: "Home",
  components: { Card },
  data() {
    return {
      PokemonList: [],
      Pokedex: [],
      imgURL:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/",
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
    },
    pokemonInterval() {
      let interval = {
        limit: 500,
        offset: 0,
      };

      return interval;
    },
    getPokemonData(id, name, url) {
      axios.get(`${url}`).then((res) => {
        let pokemon = this.setPokemon(id, name, res);
        this.setLocalStorage(pokemon);
        alert((pokemon.name + " capturado!").toUpperCase());
      });
    },
    setLocalStorage(pokemon) {
      this.Pokedex = localStorage.getItem("Pokedex");

      if (this.Pokedex) {
        this.Pokedex = JSON.parse(this.Pokedex);
        this.Pokedex.push(pokemon);
        this.Pokedex.sort(this.compareId);
      } else {
        this.Pokedex = [pokemon];
      }

      localStorage.setItem("Pokedex", JSON.stringify(this.Pokedex));
    },
    compareId(element1, element2) {
      if (element1.id > element2.id) {
        return 1;
      } else if (element1.id < element2.id) {
        return -1;
      }
    },
    setPokemon(id, name, res) {
      let info = {
        id: id,
        name: name,
        image: res.data.sprites.front_default,
        hp: res.data.stats[0].base_stat,
        attack: res.data.stats[1].base_stat,
        defense: res.data.stats[2].base_stat,
        speed: res.data.stats[5].base_stat,
        weight: res.data.weight,
        height: res.data.height,
        types: [],
        moves: [],
      };

      res.data.moves.forEach((element) => {
        info.moves.push(element.move.name);
      });

      res.data.types.forEach((element) => {
        info.types.push(element.type.name);
      });

      return info;
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
