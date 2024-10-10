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

@keyframes heartBeat {
    0% {
        transform: scale(1);
    }
    50% {
        transform: scale(1.2);
    }
    100% {
        transform: scale(1);
    }
}

.heart {
    position: absolute;
    width: 20px; /* Ajuste o tamanho conforme necessário */
    height: 20px;
    background-color: #d81b60; /* Cor do coração */
    clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); /* Forma de coração */
    animation: heartBeat 1s infinite; /* Animação de batimento */
    opacity: 0.7; /* Levemente transparente */
}

</style>
