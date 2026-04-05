<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { activate } from '__PRODUCT_NAME__'

const status = ref('Initializing...')
const licenseString = ref('')
const isReady = ref(false)

onMounted(async () => {
  try {
    const module = await import('__PRODUCT_NAME__')
    await module.default()
    isReady.value = true
    status.value = 'WASM module loaded. Paste a license below to activate.'
  } catch (e: any) {
    status.value = `Failed to load WASM module: ${e.message}`
  }
})

async function handleActivate() {
  try {
    activate('__PRODUCT_NAME__-app', licenseString.value)
    status.value = 'License activated!'
  } catch (e: any) {
    status.value = `Activation failed: ${e.message}`
  }
}
</script>

<template>
  <section id="center">
    <h1>__PRODUCT_NAME__</h1>
    <p class="status">{{ status }}</p>

    <div v-if="isReady" class="license-form">
      <textarea
        v-model="licenseString"
        placeholder="Paste your license JSON here..."
        rows="6"
      ></textarea>
      <button @click="handleActivate" :disabled="!licenseString">
        Activate License
      </button>
    </div>

    <div id="__PRODUCT_NAME__-app"></div>
  </section>
</template>

<style scoped>
#center {
  max-width: 640px;
  margin: 2rem auto;
  text-align: center;
  font-family: system-ui, sans-serif;
}

h1 {
  font-size: 2rem;
  margin-bottom: 0.5rem;
}

.status {
  color: #888;
  margin-bottom: 1.5rem;
}

.license-form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 2rem;
}

textarea {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-family: monospace;
  font-size: 0.85rem;
  resize: vertical;
}

button {
  padding: 0.75rem 1.5rem;
  background: #4f46e5;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  cursor: pointer;
}

button:hover {
  background: #4338ca;
}

button:disabled {
  background: #ccc;
  cursor: not-allowed;
}
</style>
