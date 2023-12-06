<template>
  <div>
    <MainNavbar @filter-pokemons="handleFilterPokemons" />
    <Container>
      <div class="card-container">
        <template v-if="isLoading">
          <!-- Se estiver carregando, exiba placeholders -->
          <div
              v-for="index in 200"
              :key="index"
              class="pokemon-card-placeholder"
          >
            <!-- Placeholders -->
          </div>
        </template>
        <template v-else>
          <!-- Renderiza os cards -->
          <div
              v-for="(pokemon, key) in chunkedPokemons"
              :key="key"
              class="card-row"
          >
            <MainCard
                v-for="(item, index) in pokemon"
                :key="index"
                :pokemonName="item.name"
                :pokemonUrlImage="item.url"
                :pokemonType="item.types"
            />
          </div>
        </template>
      </div>
    </Container>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import MainNavbar from './components/MainNavbar/index.vue';
import MainCard from './components/MainCard/index.vue';
import axios from 'axios';

export default {
  components: {
    MainNavbar,
    MainCard,
  },

  computed: {
    // Método computado para dividir os pokemons em grupos de 4
    chunkedPokemons() {
      const chunkSize = 4;
      const arrayCopy = [...this.pokemons];
      const chunkedArray = [];

      while (arrayCopy.length > 0) {
        chunkedArray.push(arrayCopy.splice(0, chunkSize));
      }

      return chunkedArray;
    },
  },
  setup() {
    const pokemons = ref([]);
    const searchTerm = ref('');
    const isLoading = ref(true);

    const getPokemons = () => {
      isLoading.value = true;
      const endpoints = [];
      for (let i = 1; i < 200; i++) {
        endpoints.push(`https://pokeapi.co/api/v2/pokemon/${i}/`);
      }

      const requests = endpoints.map((endpoint) => axios.get(endpoint));

      Promise.all(requests)
          .then((responses) => {
            const fetchedPokemons = responses.map((response) => ({
              name: response.data.name,
              url: response.data.sprites.front_default,
              types: response.data.types.map((typeData) => typeData.type.name),
            }));
            pokemons.value = fetchedPokemons;
            isLoading.value = false;
          })
          .catch((error) => {
            console.error(error);
          });
    };

    const handleFilterPokemons = (name) => {
      if (name === '') {
        getPokemons();
      }
      const filteredPokemons = pokemons.value.filter((pokemon) =>
          pokemon.name.includes(name)
      );
      pokemons.value = filteredPokemons;
    };

    onMounted(() => {
      getPokemons();
    });

    return {
      pokemons,
      isLoading,
      handleFilterPokemons,
    };
  },
};
</script>

<style>
.pokemon-card-placeholder {
  /* Estilos para o espaço reservado do cartão de Pokémon */
  border: 1px solid #e0e0e0;
  padding: 16px;
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  height: 100%;
}

.pokemon-image-placeholder {
  /* Estilos para o espaço reservado da imagem do Pokémon */
  width: 200px;
  height: 200px;
  background-color: #f0f0f0;
  border-radius: 50%;
}

.pokemon-info-placeholder {
  /* Estilos para o espaço reservado das informações do Pokémon */
  width: 100%;
  margin-top: 16px;
}

.pokemon-name-placeholder {
  /* Estilos para o espaço reservado do nome do Pokémon */
  height: 20px;
  background-color: #f0f0f0;
  margin-bottom: 8px;
}

.pokemon-type-placeholder {
  /* Estilos para o espaço reservado do tipo do Pokémon */
  height: 16px;
  background-color: #f0f0f0;
  margin-bottom: 8px;
}

.pokemon-description-placeholder {
  /* Estilos para o espaço reservado da descrição do Pokémon */
  height: 60px;
  background-color: #f0f0f0;
}

/* Adicione os estilos para o contêiner dos cards */
.card-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

/* Estilos para cada linha de cards */
.card-row {
  display: flex;
  justify-content: space-between;
  width: 100%;
}
</style>