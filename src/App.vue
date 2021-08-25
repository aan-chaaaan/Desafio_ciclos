<template>
  <div id="app">
    <img
      class="pokemon_logo"
      src="./assets/1200px-International_Pokémon_logo.svg.webp"
      alt="pokeImage"
    />
    <h1>Pokeguía</h1>
    <label class="label">Nombre</label>
    <input class="inputPoke" type="text" v-model="search" />
    <button @click="searchPoke" class="poke_button">Buscar</button>

    <p class="name_poke" v-for="(infoPoke, index) in infoPokes" :key="index">
      {{ infoPoke.name }}
    </p>
    <img class="image-poke" :src="showImage" alt="image-poke" />
    <h1 class="features">Habilidades</h1>
    <p>
      {{ showAbility }}
    </p>
    <br />
    <h1 class="features">Movimientos</h1>
    <p>
      {{ showMoves }}
    </p>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      infoPokes: null,
      search: "",
    };
  },
  created() {
    this.showInfoPikachu();
  },
  methods: {
    searchPoke() {
      this.showInfoPoke();
    },
    showInfoPikachu() {
      fetch("https://pokeapi.co/api/v2/pokemon/pikachu")
        .then((response) => {
          return response.json();
        })
        .then((json) => {
          this.infoPokes = json;
        });
    },
    showInfoPoke() {
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.search}`)
        .then((response) => {
          return response.json();
        })
        .then((json) => {
          this.infoPokes = json;
        });
    },
  },

  computed: {
    showImage() {
      return this.infoPokes.sprites.front_default;
    },
    showAbility() {
      return this.infoPokes.abilities[`0`].ability.name;
    },
    showMoves() {
      return this.infoPokes.moves[`0`].move.name;
    },
  },
};
</script>

<style lang="scss" scoped>
.pokemon_logo {
  width: 500px;
  display: block;
  position: relative;
  margin-left: 420px;
  margin-bottom: 40px;
}

.label {
  margin: 10px;
  margin-left: 500px;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-weight: 700;
  font-size: 20px;
  color: lightseagreen;
}

.inputPoke {
  margin: 10px;
  height: 20px;
  border-color: aquamarine;
}
.poke_button {
  width: 80px;
  height: 50px;
  margin: 10px;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-weight: 600;
  color: white;
  font-size: 17px;
  background-color: rgb(255, 136, 191);
  border-radius: 10%;
  border-color: dodgerblue;
}
h1 {
  text-align: center;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-size: 50px;
  color: cadetblue;
}
p {
  text-align: center;
  font-size: 20px;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
.image-poke {
  width: 150px;
  margin-left: 600px;
}
h3 {
  text-align: center;
}
.features {
  text-align: center;
}
</style>
