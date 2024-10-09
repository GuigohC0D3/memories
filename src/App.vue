<template>
  <div id="app">
      <header class="app-header">
          <h1>Diário de Memórias</h1>
      </header>
      <HomePage/>
  </div>
</template>

<script>
import HomePage from './views/HomePage.vue'

export default {
  components: {
    HomePage      
  },
  methods: {
      refreshMemories() {
          this.$refs.memoryList.fetchMemories();
      },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
.app-header {
  background-color: #d24d94;
  color: white;
  text-align: center;
  padding: 20px;
  border-radius: 0 0 10px 10px;
}
h1 {
  font-family: 'Pacifico', cursive;
}
</style>
