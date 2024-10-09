<template>
    <div class="homepage">
        <div v-for="heart in hearts" :key="heart.id" :style="heart.style" class="heart"></div>
        <header class="homepage-header">
            <h1>Bem-vindo ao Diário de Memórias</h1>
            <p>Capture e compartilhe nossos momentos especiais.</p>
        </header>
        <MemoryForm @refresh="refreshMemories" />
        <MemoryList ref="memoryList" />
    </div>
</template>

<script>
import MemoryForm from '../components/MemoryForm.vue';
import MemoryList from '../components/MemoryList.vue';

export default {
    components: {
        MemoryForm,
        MemoryList,
    },
    methods: {
        refreshMemories() {
            this.$refs.memoryList.fetchMemories();
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
h1 {
    color: #d81b60; /* Cor do título */
    font-family: 'Pacifico', cursive; /* Fonte estilizada */
}
p {
    color: #880e4f; /* Cor do texto */
}
</style>
