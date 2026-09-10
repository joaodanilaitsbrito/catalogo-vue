<script setup>
defineProps(['modelValue'])
defineEmits(['update:modelValue'])
</script>

<template>
  <div class="search-container">
    <input
      type="text"
      class="search-input"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      placeholder="Buscar por título ou autor..."
    />
  </div>
</template>

<style scoped>
.search-container {
  width: 100%;
}

.search-input {
  width: 100%;
  padding: 14px 18px;
  font-size: 0.95rem;
  border: 1.5px solid #d9e2ec;
  border-radius: 8px;
  outline: none;
  box-sizing: border-box;
  transition: border-color 0.2s ease, box-shadow 0.2s ease;
  color: #334e68;
}

.search-input:focus {
  border-color: #334e68;
  box-shadow: 0 0 0 3px rgba(51, 78, 104, 0.15);
}

.search-input::placeholder {
  color: #9fb3c8;
}
</style>