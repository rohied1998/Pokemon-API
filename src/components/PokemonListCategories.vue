<template>
  <div>
    <b-form-select v-model="selected" :options="options" v-on:change="sort()"></b-form-select>
    <p v-html="testData"></p>
    <div class="list">
      <article
        v-for="(pokemon, index) in pokemons"
        :key="'poke'+index"
        @click="setPokemonUrl(pokemon.url)"
      >
        <img :src="imageUrl + pokemon.id + '.png'" width="96" height="96" alt />
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

      // Sort options
      options: [
        { value: null, text: "Please select a categories option" },
        { value: "berries", text: "Berries" },
        { value: "contests", text: "Contests" },
        { value: "encounters", text: "Encounters" },
        { value: "evolution", text: "Evolution" },
        { value: "games", text: "Games" },
        { value: "items", text: "Items" },
        { value: "locations", text: "Locations" },
        { value: "machines", text: "Machines" },
        { value: "moves", text: "Moves" },
        { value: "pokemons", text: "Pokemons" }
      ]
    };
  },
  methods: {
    sort() {
      switch (this.selected) {
        case "berries":
this.pokemons.sort((a, b) => (a.name > b.name ? 1 : -1));
          break;
        case "contests":
this.pokemons.sort((a, b) => (a.name > b.name ? 1 : -1));
          break;
        case "encounters":
          this.pokemons.sort((a, b) => (a.name > b.name ? 1 : -1));
          break;
        case "evolution":
          this.pokemons.sort((a, b) => (a.name < b.name ? 1 : -1));
          break;
        case "games":
          this.pokemons.sort((a, b) => (a.name < b.name ? 1 : -1));
          break;
        case "items":
          this.pokemons.sort((a, b) => (a.name < b.name ? 1 : -1));
        break;
        case "locations":
          this.pokemons.sort((a, b) => (a.name < b.name ? 1 : -1));
        break;
        case "machines":
          this.pokemons.sort((a, b) => (a.name < b.name ? 1 : -1));
        break;
        case "moves":
          this.pokemons.sort((a, b) => (a.name < b.name ? 1 : -1));
        break;
        case "pokemons":
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
          this.nextUrl = data.next;
          data.results.forEach((pokemon, index) => {
            if (index > 9) return;
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
    scrollTrigger() {
      const observer = new IntersectionObserver(entries => {
        entries.forEach(entry => {
          if (entry.intersectionRatio > 0 && this.nextUrl) {
            this.next();
          }
        });
      });

      observer.observe(this.$refs.infinitescrolltrigger);
    },
    next() {
      this.currentUrl = this.nextUrl;
      this.fetchData();
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
  created() {
    this.currentUrl = this.apiUrl;
    this.fetchData();
  },
  mounted() {
    this.scrollTrigger();
  }
};
</script>

<style scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;
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

