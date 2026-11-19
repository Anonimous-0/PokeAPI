<script setup>
import { obtenerPokemon, obtenerDebilidades, aleatorio } from './api/pokeapi.js';
import { onMounted, ref } from "vue"

let pokemon = ref("")
let debil = ref([])
let n = ref(0)

onMounted(async () => {
  n.value = aleatorio()
  pokemon.value = await obtenerPokemon(n.value)
  debil.value = await obtenerDebilidades(pokemon.value.types[0].type.url)
  
})

</script>

<template>
  <div>
    <h1>{{ pokemon.name }}</h1>
    <div>
      <ul>
        <li v-for="(item, i) in debil.damage_relations?.double_damage_from" :key="i">{{ item.name }}</li>
      </ul>
    </div>
  </div>
</template>