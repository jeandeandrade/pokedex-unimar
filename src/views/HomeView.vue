<script setup>

// props - onMounted, reactive, ref
import { onMounted, reactive, ref } from 'vue';
import  PokemonList  from '../components/PokemonList.vue';

let pokemons = reactive(ref())

// fetch - axios
onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon?limit=20&offset=0")
  .then(response => response.json())
  .then(response => {
    pokemons.value = response.results
    console.log(pokemons)
  });
})

</script>

<template>
  <main>
    <div class="container">
      <div class="row mt-4">
        <div class="col-sm-12 col-md-6">
          <div class="card" style="width: 18rem;">
            <img src="https://assets.pokemon.com/assets/cms2/img/pokedex/full/025.png" class="card-img-top" alt="...">
            <div class="card-body">
              <h5 class="card-title">Card Title</h5>
              <p class="card-text">Um texto resumido e pequeno aqui!</p>
            </div>
          </div>
        </div>
        <div class="col-sm-12 col-md-6">
          <div class="card">
            <div class="card-body row">
              <PokemonList
                v-for="pokemon in pokemons" 
                :key="pokemon.name"
                :name="pokemon.name"
                :url="pokemon.url"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style>
/* @import url('https://fonts.googleapis.com/css?family=Acme');

main {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: radial-gradient(#156F99, #0A2E50);
  font-family: 'Acme', sans-serif;
}

.container {
  width: 90%;
}

.card {
  background-color: #fff;
  border-radius: 15px;
  box-shadow: 0px 0px 15px 0px rgba(0,0,0,0.1);
}

.pokemon-card {
  max-width: 300px;
  margin: auto;
}

.pokemon-list-card {
  padding: 15px;
}

.card-img-top {
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;
}

.card-body {
  padding: 20px;
}

.card-title {
  font-size: 1.5rem;
  font-weight: bold;
  color: #333;
}

.card-text {
  font-size: 12px;
  color: #666;
} */
</style>