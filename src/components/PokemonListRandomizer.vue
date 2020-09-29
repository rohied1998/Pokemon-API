<template>
  <div>
    <button class="random-button" @click="setPokemonUrl()">View a random Pokémon</button>
    <div class="random-item">
      <article
        v-for="(pokemon, index) in pokemons"
        :key="'poke'+index"
        @click="setPokemonUrl(pokemon.url)">
        <img :src="imageUrl + pokemon.id + '.png'" width="256" height="256" alt />
        <h5>{{ pokemon.name }}</h5>
      </article>
    </div>
  </div>
</template>

<script>
export default {
  props: ["imageUrl", "apiUrl"],
  data: () => {
    return {
      pokemons: [],
      nextUrl: "",
      currentUrl: "",

      // Selected sort option
      selected: null,


    };
  },
  methods: {
    sort() {
      switch (this.selected) {
        case "pokedex-asc":
          this.pokemons.sort((a, b) =>
            parseInt(a.id) > parseInt(b.id) ? 1 : -1
          );
          break;
        case "pokedex-des":
          this.pokemons.sort((a, b) =>
            parseInt(a.id) < parseInt(b.id) ? 1 : -1
          );
          break;
        case "a-z":
          this.pokemons.sort((a, b) => (a.name > b.name ? 1 : -1));
          break;
        case "z-a":
          this.pokemons.sort((a, b) => (a.name < b.name ? 1 : -1));
          break;
        default:
          break;
      }
    },
    fetchData() {
      const req = new Request(this.currentUrl);
      fetch(req)
        .then(resp => {
          if (resp.status === 200) return resp.json();
        })
        .then(data => {
          data.results.foreach((pokemon, index) => {
            if (index > 0) return;
            pokemon.id = pokemon.url
              .split("/")
              .filter(function(part) {
                return !!part;
              })
              .pop();
            this.pokemons.push(pokemon);
          });
        })
        .catch(error => {
          console.log(error);
        });
    },
    setPokemonUrl(url) {
      // If no url set, pick random pokemon
      if (!url) {
        url =
          "https://pokeapi.co/api/v2/pokemon/" +
          (Math.floor(Math.random() * 200) + 1).toString();
      }

      this.$emit("setPokemonUrl", url);
    }
  },
    fetchRandomData() {
      const req = new Request(this.currentUrl);
      fetch(req)
        .then(resp => {
          if (resp.status === 200) return resp.json();
        })
        .then(data => {
          this.nextUrl = data.next;
          data.results.forEach((pokemon, index) => {
            if (index > 0) return;
            pokemon.id = pokemon.url
              .split("/")
              .filter(function(part) {
                return !!part;
              })
              .pop();
            this.pokemons.push(pokemon);
          });
        })
        .catch(error => {
          console.log(error);
        });
        },
    created() {
        this.currentUrl = this.apiUrl;
        this.fetchData();
    },

    };
</script>

<style scoped>
.random-item {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 256px;
  height: 256px;
  
}
.list article {
  height: 150px;
  background-color: #efefef;
  font-size: 0.5rem;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
.list article h3 {
  margin: 0;
}
#scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 150px;
  font-size: 2rem;
  color: #efefef;
}

.random-button {
  width: 100%;
  margin: 20px 0;
  background-color: #efefef;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}

.h3 {
  font-size: 1rem;
}
</style>

