<template>
    <div class="memory-form">
        <h2>Adicionar Memória</h2>
        <form @submit.prevent="addMemory">
            <input type="text" v-model="title" placeholder="Título" required class="input-field" />
            <textarea v-model="description" placeholder="Descrição" required class="textarea-field"></textarea>
            <input type="date" v-model="date" required class="date-input" />
            <input type="file" @change="onFileChange" accept="image/*" class="file-input" />
            <button type="submit" class="submit-button">Adicionar</button>
        </form>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            title: '',
            description: '',
            date: '',
            media: null,
        };
    },
    methods: {
        onFileChange(e) {
            this.media = e.target.files[0];
        },
        async addMemory() {
            const formData = new FormData();
            formData.append('title', this.title);
            formData.append('description', this.description);
            formData.append('date', this.date);
            formData.append('image', this.media);

            await axios.post('http://localhost:3000/api/memories', formData);
            this.title = '';
            this.description = '';
            this.date = '';
            this.media = null;
            this.$emit('refresh');
        },
    },
};
</script>

<style scoped>
.memory-form {
    background-color: #f8e3f2;
    border-radius: 10px;
    padding: 20px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
    animation: fadeIn 0.5s;
}
h2 {
    color: #d24d94;
}
.input-field, .textarea-field, .date-input, .file-input {
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
    border: 2px solid #d24d94;
    border-radius: 5px;
}
.submit-button {
    background-color: #d24d94;
    color: white;
    border: none;
    padding: 10px 15px;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
}
.submit-button:hover {
    background-color: #b13b75;
}
</style>
