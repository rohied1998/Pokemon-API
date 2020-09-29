<template>
  <div class="home">
    <div class="container">
      <h1>Pokemon Categories</h1>
      <PokemonList :imageUrl="imageUrl" :apiUrl="apiUrl" @setPokemonUrl="setPokemonUrl" />
      <PokemonDetail
        v-if="showDetail"
        :pokemonUrl="pokemonUrl"
        :imageUrl="imageUrl"
        @closeDetail="closeDetail"
      />
    </div>
  </div>
</template>

<script>
import PokemonList from "@/components/PokemonListCategories.vue";
import PokemonDetail from "@/components/PokemonDetail.vue";

export default {
  data: () => {
    return {
      imageUrl:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/",
      apiPokemonUrl: "https://pokeapi.co/api/v2/pokemon/",

      pokemonUrl: "",
      showDetail: false
    };
  },
  components: {
    PokemonList,
    PokemonDetail
  },
  methods: {
    setPokemonUrl(url) {
      this.pokemonUrl = url;
      this.showDetail = true;
    },
    closeDetail() {
      this.pokemonUrl = "";
      this.showDetail = false;
    }
  }
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Rowdies");

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  font-family: "Rowdies", arial;
  font-size: 1rem;
  font-weight: normal;
}
h1 {
  color: black;
}
</style>
