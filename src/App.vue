<script setup>

import { ref, computed } from 'vue';

const counter = ref(0)
const numerosFavorito = ref([])


const changerColor = computed(() => {
  if(counter.value === 0) {return 'zero'} 
  return counter.value > 0 ? 'positive' : 'negative'
});

const viewArray = computed(() => {
   return numerosFavorito.value.filter(data => data === counter.value).length > 0
  //return numerosFavorito.value.find(counter.value)
})

const addToFavorite = () => {
   numerosFavorito.value.push(counter.value)
}
</script>

<template>
  
  <h1>Counter reactive Vue</h1><br>

  <div class="mb-3">
    <h3 v-bind:class="changerColor" >{{ counter }}</h3>
    <div v-bind:class="'d-grid gap-2 d-md-block'">
      <button 
        v-bind:class="'btn btn-outline-success'"
        @click="counter++">
      incremento
    </button>
    <button
       v-bind:class="'btn btn-outline-danger'"
       @click="counter--"
       >
       decremento
    </button>
    <button
       v-bind:class="'btn btn-outline-info'"
       @click="counter = 0" >
       reset
    </button>
    <button 
      v-bind:class="'btn btn-outline-primary'" 
      v-bind:disabled="viewArray"
      @click="addToFavorite"
      >
     add to favorite 
    </button>
    </div>
  </div><br>

  <ul class="list-group">
    <template v-for="(data,index) in numerosFavorito" v-bind:key="index">
      <li v-if="index === 0" class="list-group-item active">{{ data }}</li>
      <li v-else class="list-group-item">{{ data }}</li> 
    </template>
  </ul>

</template>

<style>
  .zero { color: peru;}
  .negative { color: red; }
  .positive { color: green;}
</style>