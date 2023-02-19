<script setup>
  import { ref, computed } from 'vue'

  const name = 'Vue dinamico'
  /* const stylecolor = "color: blue"
  const arrayColores = ["blue", "red", "peru"]
  const activo = false

  const arrayFrutas = [
    {
        name: "Manzana",
        price: "$1.00",
        description: "Una manzana",
        stock: 0,
    },
    {
        name: "Pera",
        price: "$2.00",
        description: "Una pera",
        stock: 10,
    },
    {
        name: "Naranja",
        price: "$3.00",
        description: "Una naranja",
        stock: 20,
    },
];

  const objetoFruta = {
          name: "Manzana",
          price: "$1.00",
          description: "Una manzana",
      } */

  //metodo
  const handleClick = (menssage) => {
    console.log(menssage)
  }
  

  const counter = ref(0)
  // ref() otorga propiedades reactivas y .value devuelve el cambio
  const arrayFavoritos = ref([])

  const increment = () => {
    counter.value++ // Es igual "counter + 1"
  }

  const decrement = () => {
    counter.value-- // Es igual "counter - 1"
  }

  const reset = () => {
    counter.value = 0
  }

  const add = () => {
    arrayFavoritos.value.push(counter.value)
  }

  const bloquearBtnAdd = computed(() => {
    if(counter.value === 0) return true
    const numSearch = arrayFavoritos.value.find(num => num === counter.value)
    console.log(numSearch)
    return numSearch ? true : false
  })

  // Se recomienda usar "computed" al trabajar con datos reactivos
  const classCounter = computed( () => {
    if(counter.value === 0) {
      return 'zero' 
    }
    if(counter.value > 0) {
      return 'positive' 
    }
    if(counter.value < 0) {
      return 'negative' 
    }
  })
</script>

<!-- <template>
  <h1>Interpolacion de textos</h1>
  <h2>Hola {{ name.toUpperCase() }}</h2>
  <h2>{{ arrayColores }}</h2>
  <h2 v-bind:style="`color: ${arrayColores[2]}`">Soy azul</h2>
  <h2>{{ activo ? "Estoy activo" : "Estoy Inactivo" }}</h2>

  <p v-if="activo">Estoy</p>
  <p v-else>No estoy</p>
  
  <p v-if="activo === true">Estoy activo</p>
  <p v-else-if="activo === false">Estoy inactivo</p>
  <p v-else>Estoy indeciso</p>

  <h2 v-show="activo">Apareci v-show</h2>
  <p>=============================</p>

  <br>
  <h2>Recorrriendo Arrays</h2>
  <ul>
    <template v-for="fruta in arrayFrutas" :key="fruta.name">
      <li v-if="fruta.stock > 0">
        {{ fruta.name }} - {{ fruta.price }} - {{ fruta.description }}
      </li>
    </template>
  </ul>
  <p>=============================</p>

  <br>
  <h2>Recorrriendo Objects</h2>
  <ul>
    {{ objetoFruta }}
    <li v-for="(value, propiedad, index) in objetoFruta" :key="index">
      {{ index }} - {{ propiedad }} : {{ value }}
    </li>
  </ul>
  <p>=============================</p>

  <br>
  <h2>Methods</h2>
  <button v-on:click="handleClick('Text 1')">Activame 1</button>
  <button @click="handleClick('Text 2')">Activame 2</button>
  <p>=============================</p>

  <br>
  <h2>Modificadores de Events</h2>
  <button v-on:click.right.prevent="handleClick('Text Right')">Activame right</button>
  <button @click="handleClick('Text Left')">Activame left</button>
  <button @click.middle="handleClick('Text Middle')">Activame middle</button>
  <p>=============================</p>

  <br>
  <h2>Reactividad y Computed</h2>
  <h2 :class="classCounter">{{ counter }}</h2>
  <button @click="increment">Increment</button>
  <button @click="decrement">Decrement</button>
  <button @click="reset">Reset</button>
  <button :disabled="true">Add</button>

</template> -->
<template>
  <div class="container text-center mt-3">
    <h2>Hola {{ name.toUpperCase() }}</h2>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Increment</button>
      <button @click="decrement" class="btn btn-danger">Decrement</button>
      <button @click="reset" class="btn btn-secondary">Reset</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add</button>
    </div>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(num, index) in arrayFavoritos" :key="index">
        {{ num }}
      </li>
    </ul>
  </div>
</template>

<style>
  h1 {
    color: rgb(34, 187, 239);
  }
  .positive {
    color: green;
  }
  .negative {
    color: red;
  }
  .zero {
    color: peru;
  }
</style>