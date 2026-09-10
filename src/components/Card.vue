<script setup>
import { ref } from 'vue'

const props = defineProps(['item'])
const emit = defineEmits(['update', 'delete'])

const isEditing = ref(false)

const editedItem = ref({ ...props.item })

function startEdit() {
  editedItem.value = { ...props.item }
  isEditing.value = true
}

function saveEdit() {
  if (!editedItem.value.title || !editedItem.value.category || !editedItem.value.author) return

  emit('update', { ...editedItem.value })
  isEditing.value = false
}

function cancelEdit() {
  isEditing.value = false
}

function deleteBook() {
  if (confirm('Tem certeza que deseja excluir este livro?')) {
    emit('delete', props.item.id)
  }
}
</script>

<template>
  <div class="card">
    <div v-if="!isEditing" class="card-view">
      <div class="card-header">
        <h3 class="card-title">{{ item.title }}</h3>
        <span
          class="badge"
          :class="{
            'badge-disponivel': item.status === 'Disponível',
            'badge-emprestado': item.status === 'Emprestado',
            'badge-reservado': item.status === 'Reservado'
          }"
        >
          {{ item.status }}
        </span>
      </div>
      <div class="card-body">
        <p class="card-text">
          <span class="label">Categoria:</span> {{ item.category }}
        </p>
        <p class="card-text">
          <span class="label">Autor:</span> {{ item.author }}
        </p>
      </div>
      <div class="card-actions">
        <button class="btn-edit" @click="startEdit">Editar</button>
        <button class="btn-delete" @click="deleteBook">Excluir</button>
      </div>
    </div>

    <div v-else class="card-edit">
      <input v-model="editedItem.title" class="form-control" placeholder="Título" />
      <input v-model="editedItem.category" class="form-control" placeholder="Categoria" />
      <input v-model="editedItem.author" class="form-control" placeholder="Autor" />
      <select v-model="editedItem.status" class="form-control select-control">
        <option value="Disponível">Disponível</option>
        <option value="Emprestado">Emprestado</option>
        <option value="Reservado">Reservado</option>
      </select>
      <div class="card-actions">
        <button class="btn-save" @click="saveEdit">Salvar</button>
        <button class="btn-cancel" @click="cancelEdit">Cancelar</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  background: #ffffff;
  border-radius: 12px;
  padding: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.04);
  border: 1px solid #e2e8f0;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 14px;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.08);
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 8px;
}

.card-title {
  margin: 0;
  font-size: 1.15rem;
  font-weight: 700;
  color: #102a43;
  line-height: 1.3;
}

.card-body {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.card-text {
  margin: 0;
  font-size: 0.9rem;
  color: #486581;
}

.label {
  font-weight: 600;
  color: #334e68;
}

.badge {
  font-size: 0.75rem;
  font-weight: 700;
  padding: 4px 8px;
  border-radius: 6px;
  text-transform: uppercase;
  letter-spacing: 0.04em;
  white-space: nowrap;
}

.badge-disponivel {
  background-color: #def7ec;
  color: #03543f;
}

.badge-emprestado {
  background-color: #fde8e8;
  color: #9b1c1c;
}

.badge-reservado {
  background-color: #fef08a;
  color: #713f12;
}

.card-actions {
  display: flex;
  gap: 8px;
  margin-top: 8px;
}

.btn-edit,
.btn-delete,
.btn-save,
.btn-cancel {
  flex: 1;
  padding: 8px 12px;
  border: none;
  border-radius: 6px;
  font-size: 0.85rem;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.2s ease, transform 0.1s ease;
}

.btn-edit {
  background-color: #e0e7ff;
  color: #3730a3;
}

.btn-edit:hover {
  background-color: #c7d2fe;
}

.btn-delete {
  background-color: #fde8e8;
  color: #9b1c1c;
}

.btn-delete:hover {
  background-color: #fbd5d5;
}

.btn-save {
  background-color: #def7ec;
  color: #03543f;
}

.btn-save:hover {
  background-color: #bcfce4;
}

.btn-cancel {
  background-color: #f1f5f9;
  color: #475569;
}

.btn-cancel:hover {
  background-color: #e2e8f0;
}

.card-edit {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.form-control {
  padding: 10px 12px;
  font-size: 0.9rem;
  border: 1.5px solid #d9e2ec;
  border-radius: 8px;
  outline: none;
  background-color: #f8fafc;
  color: #334e68;
  box-sizing: border-box;
  width: 100%;
}

.form-control:focus {
  background-color: #ffffff;
  border-color: #334e68;
  box-shadow: 0 0 0 3px rgba(51, 78, 104, 0.12);
}

.select-control {
  cursor: pointer;
}
</style>