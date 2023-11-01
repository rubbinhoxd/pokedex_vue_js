<template>
  <div class="main-navbar">
    <img src="/assets/pokebola.png" height="4em" />
    <h6 class="title">Pokédex</h6>
    <div class="search">
      <div class="search-icon">
        <i class="material-icons">search</i>
      </div>
      <input
          v-model="searchQuery"
          type="text"
          placeholder="Pesquisando.."
          @input="handleFilterPokemons"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: '',
    };
  },
  methods: {
    handleFilterPokemons() {
      this.$emit('filter-pokemons', this.searchQuery);
    },
  },
};
</script>

<style scoped>
.main-navbar {
  display: flex;
  align-items: center;
  background-color: white;
  margin-bottom: 1em;
  padding: 1em;
  /* Estilos do seu componente MainNavbar Vue aqui */
}

.main-navbar img {
  height: 4em;
  margin-right: 1em;
}

.main-navbar .title {
  flex-grow: 1;
  display: none;
  color: black;
  margin-left: 1em;
}

.main-navbar .search {
  position: relative;
  background-color: black;
  color: white;
  border-radius: 4px;
  width: 100%;
}

.main-navbar .search-icon {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  top: 0;
  bottom: 0;
  left: 0;
  padding: 0.5em;
}
</style>