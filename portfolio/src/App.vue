<script setup>
import { RouterView } from 'vue-router'
import Home from './components/Home.vue';
import HeaderApp from './components/Header.vue';
import Footer from './components/Footer.vue';
</script>

<template>
  <RouterView/>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Rubik:ital,wght@0,300..900;1,300..900&display=swap');

* {
  font-family: "Rubik", sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>