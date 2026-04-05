<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { activate } from '__PRODUCT_NAME__'

const status = ref('Initializing...')

onMounted(async () => {
  try {
    const module = await import('__PRODUCT_NAME__')
    await module.default()
    status.value = 'WASM module loaded. Attempting auto-activation...'

    // The WASM SDK will look for the license at __NAMESPACE__/license.json
    // relative to the public directory. Place your license file there.
    activate('__PRODUCT_NAME__-auto-app')
    status.value = 'License activated automatically from __NAMESPACE__/license.json'
  } catch (e: any) {
    status.value = `Auto-activation failed: ${e.message}`
  }
})
</script>

<template>
  <section class="auto-load-section">
    <h2>Auto-load License</h2>
    <p class="description">
      This component loads the license automatically from
      <code>public/__NAMESPACE__/license.json</code>.
      Place your license file there and the WASM SDK will find it.
    </p>
    <p class="status">{{ status }}</p>
    <div id="__PRODUCT_NAME__-auto-app"></div>
  </section>
</template>

<style scoped>
.auto-load-section {
  max-width: 640px;
  margin: 2rem auto;
  text-align: center;
  font-family: system-ui, sans-serif;
  padding: 1.5rem;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  background: #f9fafb;
}

h2 {
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
}

.description {
  color: #666;
  font-size: 0.9rem;
  margin-bottom: 1rem;
}

.description code {
  background: #e5e7eb;
  padding: 0.15rem 0.4rem;
  border-radius: 3px;
  font-size: 0.85rem;
}

.status {
  color: #888;
  font-style: italic;
}
</style>
