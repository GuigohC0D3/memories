<template>
    <div class="memory-list">
        <h2>Timeline Romance</h2>
        <div v-for="memory in memories" :key="memory.id" class="memory-item">
            <h3>{{ memory.title }}</h3>
            <p>{{ memory.description }}</p>
            <p class="memory-date">{{ new Date(memory.date).toLocaleDateString() }}</p>
            <img v-if="memory.image" :src="'http://localhost:3000/' + memory.image" class="memory-media" />
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            memories: [],
        };
    },
    async created() {
        await this.fetchMemories();
    },
    methods: {
        async fetchMemories() {
            const response = await axios.get('http://localhost:3000/api/memories');
            this.memories = response.data;
        },
    },
};
</script>

<style scoped>
.memory-list {
    animation: fadeIn 0.5s;
    margin-top: 20px;
}

h2 {
    color: #d81b60; /* Cor do título */
    margin-bottom: 10px;
}

.memory-item {
    background-color: #fff3f6; /* Cor de fundo dos itens */
    border: 1px solid #d81b60; /* Cor das bordas */
    border-radius: 10px;
    padding: 15px;
    margin: 15px 0;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.memory-media {
    width: 100px; /* Largura fixa */
    height: 100px; /* Altura fixa */
    object-fit: cover; /* Corta a imagem para caber sem distorcer */
    border-radius: 5px;
    margin-top: 10px;
}

.memory-date {
    font-size: 0.8em;
    color: #880e4f; /* Cor do texto da data */
}
</style>
