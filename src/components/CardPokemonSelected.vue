<script setup>
const pokemon = defineProps([
  "name",
  "xp",
  "height",
  "weight",
  "image",
  "loading",
]);
</script>

<template>
  <div
    class="card card-pokemon-selected"
    :class="loading ? null : 'animate__animated animate__flipInX'"
    v-if="pokemon.name"
  >
    <img
      v-if="pokemon.name"
      :src="pokemon.image"
      class="card-img-top pt-2"
      :class="loading ? null : 'animate__animated animate__rubberBand'"
      height="250"
      alt="Imagem do pokemon selecionado"
    />

    <img
      v-else
      src="../assets/egg_pokemon.svg"
      class="card-img-top pt-2"
      height="250"
      alt="Imagem do pokemon selecionado"
    />

    <div class="card-body">
      <h4 class="card-title text-center">
        {{ pokemon.name || "???" }}
      </h4>

      <hr />

      <div class="row">
        <section class="col">
          <strong>XP: </strong>
          <span>{{ pokemon.xp }}</span>
        </section>

        <section class="col">
          <strong>Peso: </strong>
          <span>{{ pokemon.weight }}</span>
        </section>

        <section class="col">
          <strong>Altura: </strong>
          <span>{{ pokemon.height }}</span>
        </section>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card-pokemon-selected {
  height: 83vh;
  background: rgb(72, 63, 251);
  background: radial-gradient(
    circle,
    rgba(72, 63, 251, 0.6) 0%,
    rgba(70, 252, 244, 0.4) 100%
  );
}

@media (max-width: 600px) {
  .card-pokemon-selected {
    height: 100%;
  }
}
</style>
