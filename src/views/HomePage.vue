<template>
    <div class="homepage">
        <header class="homepage-header">
            <h1>Bem-vindo ao Diário de Memórias</h1>
            <p>Capture e compartilhe nossos momentos especiais.</p>
        </header>

        <button @click="toggleForm" class="add-memory-btn">
            Adicionar nova memória
        </button>

        <MemoryForm v-if="showForm" @memoryAdded="addMemory" />

        <MemoryList ref="memoryList" :memories="memories" />
    </div>
</template>

<script>
import MemoryForm from '../components/MemoryForm.vue';
import MemoryList from '../components/MemoryList.vue';
import axios from 'axios';

export default {
    components: {
        MemoryForm,
        MemoryList,
    },
    data() {
        return {
            showForm: false,
            memories: [],
        };
    },
    async created() {
        await this.fetchMemories();
    },
    methods: {
        toggleForm() {
            this.showForm = !this.showForm;
        },
        async fetchMemories() {
            const response = await axios.get('http://localhost:3000/api/memories');
            this.memories = response.data;
        },
        async addMemory() {
            await this.fetchMemories(); // Recarrega a lista de memórias após adicionar
            this.createHeartAnimation(); // Chama a animação do coração
        },
        createHeartAnimation() {
            const heart = document.createElement('div');
            heart.classList.add('heart');
            document.body.appendChild(heart); // Adiciona o coração ao corpo do documento

            // Define uma posição aleatória para o coração
            heart.style.left = Math.random() * window.innerWidth + 'px';
            heart.style.top = Math.random() * window.innerHeight + 'px';

            // Remove o coração após a animação
            setTimeout(() => {
                heart.remove();
            }, 1000); // Dura 1 segundo
        },
    },
};
</script>

<style scoped>
.homepage {
  padding: 20px;
  background-color: #fce4ec; /* Cor de fundo suave */
}
.homepage-header {
  text-align: center;
  margin-bottom: 20px;
}
.add-memory-btn {
  background-color: #e6178f;
  color: white;
  padding: 10px 20px;
  margin-bottom: 20px;
  border: none;
  cursor: pointer;
}
.add-memory-btn:hover {
  background-color: #c7056f;
}
</style>
