<script>
export default {
  name: 'Boolflix',
  data() {
    return {
      searchWord: ''
    }
  }
}
</script>

<template>
  <!-- # Search Bar -->
  <form>
    <input type="text" placeholder="Cerca..." v-model.trim="searchWord">
    <button type="button">Cerca</button>
  </form>
</template>

<style>
body {
  background-color: #0d1117;
  color: #f0f6fc;
  min-height: 100vh;
  padding: 20px;
}
</style>