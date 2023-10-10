<script setup>
import { ref, computed } from "vue";
const name = " Vue js ";
const styleColor1 = "color: red;";
const styleColor2 = "color: green;";
const favNumArray = ref([]);

const counter = ref(0);

const increment = () => counter.value++;

const decrement = () => counter.value--;

const reset = () => (counter.value = 0);

const add = () => {
  favNumArray.value.push(counter.value);
};

const blockAdd = computed(() => {
  const numSearch = favNumArray.value.find((num) => num === counter.value);
  //if (numSearch === 0 ) return true;
  //return numSearch ? true : false;
  //estas lineas se puede resumir con esta siguiente
  return numSearch || numSearch === 0;
});

const classCounter = computed(() => {
  if (counter.value === 0) {
    return "zero";
  }
  if (counter.value > 0) {
    return "positive";
  }
  if (counter.value < 0) {
    return "negative";
  }
});
</script>

<template>
  <div class="container text-center" mt-4>
    <h1>{{ name.toUpperCase() }} :) </h1>
    <h2 :class="classCounter">{{ counter }}</h2>

    <div class="btn-group">
      <button @click="increment" class="btn btn-outline-success">Aumentar</button>
      <button @click="decrement" class="btn btn-outline-warning">Disminuye</button>
      <button @click="reset" class="btn btn-outline-dark">Reset</button>
      <button @click="add" :disabled="blockAdd" class="btn btn-outline-info">
        Add to favorites </button>
    </div>

    <ul class="list-group mt-4" >
      <li
        class="list-group-item"
        v-for="(num, index) in favNumArray"
        :key="index"
      >
        {{ num }}
      </li>
    </ul>
  </div>
</template>

<style>
h1 {
  color: rgb(68, 42, 141);
}

.positive {
  color: rgb(90, 216, 90);
}

.negative {
  color: rgb(167, 67, 67);
}

.zero {
  color: grey;
}
</style>
