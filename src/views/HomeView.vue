<script setup>
import ListPokemons from "@/components/ListPokemons.vue";
import CardPokemonSelected from "@/components/CardPokemonSelected.vue";

import { onMounted, reactive, ref, computed } from "vue";

let urlBaseSvg = ref(
  "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/"
);
let pokemons = reactive(ref());
let searchPokemonField = ref("");
let pokemonSelected = reactive(ref());
let loading = ref(false);

onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
    .then((res) => res.json())
    .then((res) => (pokemons.value = res.results))
    .catch((error) => {
      console.error("Erro ao buscar os dados:", error);
    });
});

const pokemonFiltered = computed(() => {
  if (pokemons.value && searchPokemonField.value) {
    return pokemons.value.filter((pokemon) =>
      pokemon.name
        .toLowerCase()
        .includes(searchPokemonField.value.toLowerCase())
    );
  }
  return pokemons.value;
});

const selectPokemon = async (pokemon) => {
  loading.value = true;

  await fetch(pokemon.url)
    .then((res) => res.json())
    .then((res) => (pokemonSelected.value = res))
    .catch((err) =>
      alert(
        "Estamos com problemas para processar sua solicitação, por favor tente novamente",
        err
      )
    )
    .finally(() => (loading.value = false));
};
</script>

<template>
  <main>
    <div class="container">
      <div class="row mt-4">
        <div class="col-sm-12 col-md-6 cards">
          <CardPokemonSelected
            :image="pokemonSelected?.sprites.other.dream_world.front_default"
            :name="pokemonSelected?.name"
            :xp="pokemonSelected?.base_experience"
            :height="pokemonSelected?.height"
            :weight="pokemonSelected?.weight"
            :loading="loading"
          />
        </div>

        <div class="col-sm-12 cards" :class="pokemonSelected ? 'col-md-6' : ''">
          <div class="card card-list">
            <div class="card-body row">
              <div class="input-group mb-3">
                <label hidden for="searchPokemonField" class="form-label">
                  Pesquisar Pokémon...
                </label>

                <input
                  v-model="searchPokemonField"
                  type="text"
                  class="form-control"
                  id="searchPokemonField"
                  placeholder="Busque por um Pokémon..."
                />
              </div>

              <ListPokemons
                @click="selectPokemon(pokemon)"
                v-for="pokemon in pokemonFiltered"
                :key="pokemon.name"
                :name="pokemon.name"
                :urlBaseSvg="urlBaseSvg + pokemon.url.split('/')[6] + '.svg'"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.card-list {
  max-height: 83vh;
  overflow-y: scroll;
  overflow-x: hidden;
}

@media (max-width: 600px) {
  .cards + .cards {
    margin-top: 1.5rem;
  }
}
</style>
