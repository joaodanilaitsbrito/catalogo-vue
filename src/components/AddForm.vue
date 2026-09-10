<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add'])

const title = ref('')
const category = ref('')
const author = ref('')
const status = ref('Disponível')

function submit() {
  if (!title.value || !category.value || !author.value) return

  emit('add', {
    title: title.value,
    category: category.value,
    author: author.value,
    status: status.value
  })

  title.value = ''
  category.value = ''
  author.value = ''
  status.value = 'Disponível'
}
</script>

<template>
  <form class="form-container" @submit.prevent="submit">
    <div class="input-group">
      <input v-model="title" class="form-control" placeholder="Título da obra" required />
      <input v-model="category" class="form-control" placeholder="Categoria" required />
      <input v-model="author" class="form-control" placeholder="Autor" required />
      <select v-model="status" class="form-control select-control">
        <option value="Disponível">Disponível</option>
        <option value="Emprestado">Emprestado</option>
        <option value="Reservado">Reservado</option>
      </select>
    </div>
    <button type="submit" class="btn-submit">Adicionar Livro</button>
  </form>
</template>

<style scoped>
.form-container {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.input-group {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 12px;
}

.form-control {
  padding: 10px 14px;
  font-size: 0.9rem;
  border: 1.5px solid #d9e2ec;
  border-radius: 8px;
  outline: none;
  background-color: #f8fafc;
  color: #334e68;
  box-sizing: border-box;
  transition: all 0.2s ease;
}

.form-control:focus {
  background-color: #ffffff;
  border-color: #334e68;
  box-shadow: 0 0 0 3px rgba(51, 78, 104, 0.12);
}

.select-control {
  cursor: pointer;
}

.btn-submit {
  align-self: flex-end;
  padding: 11px 24px;
  background-color: #102a43;
  color: #ffffff;
  font-weight: 600;
  font-size: 0.9rem;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.2s ease, transform 0.1s ease;
}

.btn-submit:hover {
  background-color: #243b53;
}

.btn-submit:active {
  transform: translateY(1px);
}

@media (max-width: 640px) {
  .btn-submit {
    width: 100%;
  }
}
</style>