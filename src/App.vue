<template>
  <div class="root-div">
    <h1 class="text-3xl text-yellow-300 font-bold text-center pt-5">Random Game</h1>
    <MRRandomCard />
  </div>
</template>

<script setup>
import MRRandomCard from './components/MRRandomCard.vue';
</script>

<style>
.root-div {
  width: 100%;
  height: 100vh;
  background-image: linear-gradient(to right, rgb(0, 216, 180), rgb(0, 119, 255));
}
</style>