<template>
  <div class="main-card">
    <img :src="pokemonUrlImage" alt="green iguana" height="250" />
    <div class="card-content">
      <h5>{{ pokemonName }}</h5>
      <p>{{ handlePickTypesOfPokemons(pokemonType) }}</p>
      <p>
        Lizards are a widespread group of squamate reptiles, with over 6,000
        species, ranging across all continents except Antarctica
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    pokemonName: String,
    pokemonUrlImage: String,
    pokemonType: Array,
  },
  methods: {
    handlePickTypesOfPokemons(pokemonType) {
      return pokemonType.join(' | ');
    },
  },
};
</script>

<style scoped>
.main-card {
  max-width: 345px;
  /* Estilos do seu componente MainCard Vue aqui */
}

/* Estilos para o contêiner dos cards */
.card-container {
  display: flex;
  flex-wrap: wrap; /* Permite que os cards quebrem para a próxima linha */
  justify-content: space-between; /* Distribui os cards igualmente na linha */
  gap: 20px; /* Espaçamento entre os cards */
}

.main-card img {
  width: 100%;
}

.main-card .card-content {
  padding: 16px;
}
</style>