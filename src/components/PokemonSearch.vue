<template>
  <div class="searchbar">
    <form @submit.prevent="setPokemonUrl">
      <input type="text" placeholder="Search for a Pokemon" v-model="searchvalue" />
    </form>
    <i class="fas fa-search" @click="setPokemonUrl"></i>
  </div>
</template>

<script>
export default {
  props: ["apiUrl"],
  data: () => {
    return {
      searchvalue: ""
    };
  },
  methods: {
    setPokemonUrl(url) {
      if (this.searchvalue !== "")
        this.$emit("setPokemonUrl", this.apiUrl + this.searchvalue);
    }
  }
};
</script>

<style scoped>
.searchbar {
  position: relative;
  width: 100%;
  max-width: 400px;
  padding-bottom: 20px;
}
.searchbar input {
  border: none;
  outline: none;
  border-radius: 5px;
  padding: 10px 40px 10px 10px;
  width: calc(100% - 50px);
  font-size: 1rem;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
.searchbar i {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 1.25rem;
  color: #0a2e50;
  cursor: pointer;
}
</style>
