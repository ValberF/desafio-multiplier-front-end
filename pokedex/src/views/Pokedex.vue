<template>
  <div class="pokedex">
    <h1>PokéDex</h1>
    <b-container>
      <b-row align-h="around">
        <Card
          v-for="pokemon in Pokedex"
          :key="pokemon.id"
          :title="pokemon.name"
          :image="pokemon.image"
          :imgAlt="pokemon.name"
        />
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Card from "../components/Card.vue";

export default {
  name: "Pokedex",
  components: { Card },
  data() {
    return {
      Pokedex: [],
    };
  },
  methods: {
    getPokedex() {
      this.Pokedex = localStorage.getItem("Pokedex");
      this.Pokedex = JSON.parse(this.Pokedex);
    },
  },
  mounted() {
    this.getPokedex();
  },
};
</script>

<style>
.pokedex {
  display: flex;
  align-items: center;
  flex-direction: column;
}
</style>