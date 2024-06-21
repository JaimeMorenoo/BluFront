<template>
  <header class="header">
    <div class="has-text-centered">
      <h1 class="title has-text-white">Sorteo</h1>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header'
};
</script>

<style scoped>
.header {
  justify-content: space-between;
  align-items: center;
  background-color: #001f3f; /* Electric Blue */
  padding: 1rem 2rem;
  color: white;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  text-align: center;
}
</style>
