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
  margin-right: 0.5em; /* Reduz um pouco o espaçamento entre a imagem e o texto */
}

.main-navbar .title {
  flex-grow: 1;
  display: block;
  font-size: 1.5em;
  color: black;
  margin-left: 0.5em; /* Reduz o espaçamento à esquerda */
}

.main-navbar .search {
  position: relative;
  background-color: white; /* Altera a cor de fundo para branco */
  border-radius: 4px;
  width: 100%;
  border: 1px solid #ccc; /* Adiciona uma borda para destacar o campo de entrada */
}

.main-navbar .search-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.5em;
  background-color: #ccc; /* Altera a cor de fundo do ícone de pesquisa */
  border-radius: 4px 0 0 4px; /* Ajusta o raio da borda */
  color: white;
}

.main-navbar .search input {
  width: calc(100% - 2em); /* Ajusta o tamanho do input para se alinhar com o ícone de pesquisa */
  padding: 0.5em;
  border: none;
  border-radius: 0 4px 4px 0; /* Ajusta o raio da borda */
  background-color: white;
  color: #333;
}
</style>