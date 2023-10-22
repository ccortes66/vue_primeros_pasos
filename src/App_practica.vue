<script setup>
 const name = 'vue js dinamico'
 const colorAzul = 'color: blue'
 const arrayColores = ['blue','red','green','peru']
 const activo = false
 const arrayFrutas = ["naranja", "manzana", "pera", "mandarina"]
 const arrayFrutasT = [
        {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
            stock: 0
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
            stock: 30
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
            stock: 50
        },
    ];

const singleObject = {
                        name: "Naranja",
                        price: "$3.00",
                        description: "Una naranja",
                      }
//metodo click
const handleClick = () => console.info('me disite click')
const metodoConParameto = (sms) => console.warn(`menaje de advertencia ${sms}`)

import {ref, computed} from 'vue'
const counter = ref(0)
const cambiarClass = computed(() => {

  if(counter.value === 0) {return 'zero'}
  return counter.value > 0 ? 'positive' : 'negative' 
  
})
    
</script>
<template>
  <h1>Hola {{ name.toUpperCase() }}</h1><br>
  <h2>{{ arrayColores }}</h2><br>
  <h3 v-bind:style="`color: ${arrayColores[3]}`" >texto color {{ arrayColores[3] }}</h3>
  <p> {{ activo ? "Si estoy activo" : "no lo estoy" }}</p>
  <p v-if="activo === true">parrafo activo </p>
  <p v-else-if="activo === false">parafo Inactivo</p>
  <p v-else>???</p>

  <p v-show="activo"> parrafo v-show activo</p>
  <ul>
    <li v-for="(fruta,index) in arrayFrutas" v-bind:key="index">{{ index }} - {{ fruta }}</li>
  </ul>

  <ul>
    <li v-for="data in arrayFrutasT" v-bind:key="data.name">{{ data }} </li>
  </ul>

  <ul>
    <li v-for="(value,mykey) in singleObject" v-bind:key="value" > {{ mykey }} : {{ value }} </li>
  </ul>
  <ul>
    <template v-for="data in arrayFrutasT" v-bind:key="data.name" >
       <li v-if="data.stock > 0"> {{ data.name }} - {{ data.price }}</li>    
    </template>
  </ul>
  
  <div>
    <button v-on:click="handleClick">Activar</button>
    <button @click="handleClick">Activar</button>
    <button @click="metodoConParameto('AAAA')">mensajeConParametro</button>
  </div>

  <!---eventos mause vue -->
  <div>
    <button @click.right.prevent="metodoConParameto('Activar right')">Activar right</button>
    <button @click.left="metodoConParameto('Activar left')">Activar left</button>
    <button @click.middle="metodoConParameto('Activar middle')">Activar middle</button>
  </div>

  <div>
    <div>
      <button @click="counter++">add 1</button>
      <button @click="counter--">restore 1</button>
      <button @click="counter = 0">reset</button>
    </div>
    
    <p v-bind:class="cambiarClass">{{ counter }}</p>
  </div>



</template>
<style>
    h1{color: red;}
   .positive{ color: green; }
   .negative{ color: red ; }
   .zero{ color: peru ; }
</style>