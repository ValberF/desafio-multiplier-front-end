<template>
  <div class="pokedex">
    <h1>PokéDex</h1>
    <b-container>
      <b-row align-h="around">
        <ul class="list-unstyled">
          <b-media tag="li" v-for="(pokemon, index) in Pokedex" :key="index">
            <template #aside>
              <b-img
                :src="pokemon.image"
                width="64"
                :alt="pokemon.name"
              ></b-img>
            </template>
            <h5 class="mt-0 mb-1">{{ pokemon.name }}</h5>
            <b-badge :class="pokemon.types[0]">{{ pokemon.types[0] }}</b-badge>
            <b-badge :class="pokemon.types[1]">{{ pokemon.types[1] }}</b-badge>
            <b-icon
              icon="x-circle"
              @click="deletePokemon(pokemon.name, index)"
              scale="1.5"
              variant="danger"
            ></b-icon>
            <b-icon
              icon="info-circle-fill"
              v-b-modal.modal-1
              @click="pokemonTempData(pokemon)"
              scale="1.5"
              variant="success"
            ></b-icon>
            <hr />
          </b-media>
        </ul>
      </b-row>
    </b-container>
    <b-modal id="modal-1" :title="tempData.name">
      <b-img :src="tempData.image" width="150" :alt="tempData.name"></b-img>
      <b-container>
        <b-row>
          <strong>Movimentos:</strong>
          <b-list-group flush title="Movimentos:" style="max-width: 55%">
            <b-list-group-item
              v-for="(moves, index) in tempData.moves"
              :key="index"
              >{{ tempData.moves[index] }}</b-list-group-item
            >
          </b-list-group>

          <b-container class="pokemon-details" style="max-width: 40%">
            <p>Peso: {{ (tempData.weight/10) }} kg</p>
            <p>Altura: {{ (tempData.height/10) }} m</p>
            <p>Vida: {{ tempData.hp }}</p>
            <p>Ataque: {{ tempData.attack }}</p>
            <p>Defesa: {{ tempData.defense }}</p>
            <p>Velocidade: {{ tempData.speed }}</p>

          </b-container >
        </b-row>
      </b-container>
    </b-modal>
  </div>
</template>

<script>
export default {
  name: "Pokedex",
  data() {
    return {
      Pokedex: [],
      tempData: {},
    };
  },
  methods: {
    getPokedex() {
      this.Pokedex = localStorage.getItem("Pokedex");
      this.Pokedex = JSON.parse(this.Pokedex);
    },
    deletePokemon(name, id) {
      this.Pokedex.splice(id, 1);
      localStorage.setItem("Pokedex", JSON.stringify(this.Pokedex));
      alert((name + " excluído da pokedex!").toUpperCase());
    },
    pokemonTempData(pokemon) {
      this.tempData = pokemon;
      this.tempData.name = this.tempData.name.toUpperCase();
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

h1 {
  margin-bottom: 30px !important;
}

.pokedex .container {
  padding: 2rem;
  height: 70vh;
  width: 95vw;
  overflow-y: scroll;

  background-color: #fff;
  border-radius: 15px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.25);
}

.pokedex .badge:nth-child(3) {
  margin-left: 7px;
}

.pokedex svg {
  margin-left: 25px;

  float: right;
  cursor: pointer;
}

.modal-content {
  min-height: 72vh !important;
}

.list-group {
  border: solid 2px #929292;
  border-radius: 10px !important;
  overflow-y: scroll;
  height: 30vh;
  padding: 0 !important;
  font-weight: bold;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.25);
}

.pokemon-details {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  box-shadow: 0 0 10px rgba(0, 0, 0, 0.25);
  border: solid 2px #929292;
  border-radius: 10px !important;
  height: 30vh;
}

.pokemon-details p {
  font-size: smaller;
  font-weight: bold;
}

.normal {
  background-color: #a7a979;
}

.fire {
  background-color: #e87f37;
}

.fighting {
  background-color: #b92a2c;
}

.water {
  background-color: #728cef;
}

.flying {
  background-color: #aa8bef;
}

.grass {
  background-color: #7ecb53;
}

.poison {
  background-color: #9c379f;
}

.electric {
  background-color: #f3d23a;
}

.ground {
  background-color: #dcc16b;
}

.psychic {
  background-color: #f05189;
}

.rock {
  background-color: #b4a13d;
}

.ice {
  background-color: #9fd9d8;
}

.bug {
  background-color: #a7bb29;
}

.dragon {
  background-color: #751bf6;
}

.ghost {
  background-color: #705597;
}

.dark {
  background-color: #6e5849;
}

.steel {
  background-color: #b9b7d0;
}

.fairy {
  background-color: #e897ac;
}

</style>