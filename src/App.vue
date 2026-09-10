<script setup>
import { ref, computed, watch } from 'vue'
import SearchBar from './components/SearchBar.vue'
import Card from './components/Card.vue'
import AddForm from './components/AddForm.vue'

const defaultItems = [
  { id: 1, title: 'O Senhor dos Anéis', category: 'Fantasia', author: 'J.R.R. Tolkien', status: 'Disponível' },
  { id: 2, title: '1984', category: 'Distopia', author: 'George Orwell', status: 'Emprestado' },
  { id: 3, title: 'Dom Casmurro', category: 'Romance', author: 'Machado de Assis', status: 'Disponível' },
  { id: 4, title: 'Clean Code', category: 'Tecnologia', author: 'Robert C. Martin', status: 'Disponível' }
]

const savedItems = localStorage.getItem('catalogo-livros')
const items = ref(savedItems ? JSON.parse(savedItems) : defaultItems)

const searchTerm = ref('')

const filteredItems = computed(() => {
  return items.value.filter(item =>
    item.title.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
    item.author.toLowerCase().includes(searchTerm.value.toLowerCase())
  )
})

function addItem(newItem) {
  items.value.push({ id: Date.now(), ...newItem })
}

function updateItem(updatedItem) {
  const index = items.value.findIndex(i => i.id === updatedItem.id)
  if (index !== -1) {
    items.value[index] = updatedItem
  }
}

function deleteItem(id) {
  items.value = items.value.filter(i => i.id !== id)
}

watch(items, (newItems) => {
  localStorage.setItem('catalogo-livros', JSON.stringify(newItems))
}, { deep: true })
</script>

<template>
  <div class="page-wrapper">
    <div class="container">
      <header class="app-header">
        <h1 class="app-title">Catálogo de Livros</h1>
        <p class="app-subtitle">Gerencie seu acervo de leitura de forma simples e intuitiva</p>
      </header>
      <section class="section-search">
        <SearchBar v-model="searchTerm" />
      </section>
      <section class="section-form">
        <AddForm @add="addItem" />
      </section>
      <section class="section-grid">
        <div v-if="filteredItems.length === 0" class="empty-state">
          Nenhum livro encontrado com o termo pesquisado.
        </div>
        <div v-else class="grid">
          <Card
            v-for="item in filteredItems"
            :key="item.id"
            :item="item"
            @update="updateItem"
            @delete="deleteItem"
          />
        </div>
      </section>
    </div>
  </div>
</template>

<style scoped>
.page-wrapper {
  min-height: 100vh;
  width: 100%;
  background: linear-gradient(135deg, #f0f4f8 0%, #d9e2ec 100%);
  padding: 40px 16px;
  box-sizing: border-box;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  color: #243b53;
}
.container {
  max-width: 960px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 28px;
}
.app-header {
  text-align: center;
}
.app-title {
  font-size: 2.2rem;
  font-weight: 800;
  color: #102a43;
  margin: 0 0 6px 0;
  letter-spacing: -0.03em;
}
.app-subtitle {
  font-size: 1rem;
  color: #627d98;
  margin: 0;
}
.section-search,
.section-form {
  background: #ffffff;
  padding: 20px 24px;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
}
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 20px;
}
.empty-state {
  text-align: center;
  padding: 40px;
  background: #ffffff;
  border-radius: 12px;
  color: #829ab1;
  font-size: 1.05rem;
  border: 1px dashed #bcccdc;
}
@media (max-width: 640px) {
  .page-wrapper {
    padding: 20px 12px;
  }
  
  .app-title {
    font-size: 1.75rem;
  }
  
  .section-search,
  .section-form {
    padding: 16px;
  }
}
</style>
