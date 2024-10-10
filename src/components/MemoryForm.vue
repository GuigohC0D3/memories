<template>
    <form @submit.prevent="submitMemory" class="memory-form">
        <div class="form-group">
            <label for="title">Título:</label>
            <input type="text" v-model="memory.title" required />
        </div>
        <div class="form-group">
            <label for="description">Descrição:</label>
            <textarea v-model="memory.description" required></textarea>
        </div>
        <div class="form-group">
            <label for="date">Data:</label>
            <input type="date" v-model="memory.date" required />
        </div>
        <div class="form-group">
            <label for="image">Imagem:</label>
            <input type="file" @change="onFileChange" accept="image/*" /> <!-- Aceita qualquer tipo de imagem -->
        </div>
        <div class="form-buttons">
            <button type="submit" class="submit-btn">Adicionar Memória</button>
            <button type="button" class="cancel-btn" @click="resetForm">Cancelar</button>
        </div>
    </form>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            memory: {
                title: '',
                description: '',
                date: '',
                image: null,
            },
        };
    },
    methods: {
        async submitMemory() {
            try {
                const formData = new FormData();
                formData.append('title', this.memory.title);
                formData.append('description', this.memory.description);
                formData.append('date', this.memory.date);
                if (this.memory.image) {
                    formData.append('image', this.memory.image);
                }

                await axios.post('http://localhost:3000/api/memories', formData, {
                    headers: {
                        'Content-Type': 'multipart/form-data',
                    },
                });

                this.$emit('memoryAdded');
                this.resetForm();
            } catch (error) {
                console.error("Erro ao adicionar memória:", error);
            }
        },
        onFileChange(event) {
            const file = event.target.files[0];
            this.memory.image = file; // Armazena o arquivo selecionado
        },
        resetForm() {
            this.memory.title = '';
            this.memory.description = '';
            this.memory.date = '';
            this.memory.image = null;
        },

        toggleForm() {
        this.showForm = !this.showForm; // Alterna a exibição do formulário
    },
    async fetchMemories() {
        const response = await axios.get('http://localhost:3000/api/memories');
        this.memories = response.data; // Atualiza a lista de memórias
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
.memory-form {
    display: flex;
    flex-direction: column;
    margin: 20px 0;
    padding: 20px;
    background-color: #fff; /* Fundo branco */
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.form-group {
    margin-bottom: 15px; /* Espaçamento entre campos */
}

label {
    margin-bottom: 5px;
    font-weight: bold; /* Negrito para os rótulos */
}

input, textarea {
    width: 100%; /* Largura total */
    padding: 10px; /* Espaçamento interno */
    border-radius: 4px;
    border: 1px solid #ccc; /* Borda cinza clara */
}

textarea {
    resize: vertical; /* Permitir redimensionamento vertical */
}

.form-buttons {
    display: flex;
    justify-content: space-between; /* Espaçar os botões */
}

.submit-btn, .cancel-btn {
    padding: 10px 20px;
    border: 2px solid transparent; /* Borda transparente por padrão */
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s, border-color 0.3s; /* Transição suave */
}

.submit-btn {
    background-color: #4CAF50; /* Verde */
    color: white;
    border-color: #4CAF50; /* Borda verde */
}

.submit-btn:hover {
    background-color: #45a049; /* Verde escuro ao passar o mouse */
    border-color: #45a049; /* Borda verde escuro ao passar o mouse */
}

.cancel-btn {
    background-color: #f44336; /* Vermelho */
    color: white;
    border-color: #f44336; /* Borda vermelha */
}

.cancel-btn:hover {
    background-color: #d32f2f; /* Vermelho escuro ao passar o mouse */
    border-color: #d32f2f; /* Borda vermelha escura ao passar o mouse */
}
</style>
