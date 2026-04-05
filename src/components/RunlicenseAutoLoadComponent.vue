<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { activateFromLicenseFile } from '__PRODUCT_NAME__'

const status = ref('Initializing...')

onMounted(async () => {
  try {
    const module = await import('__PRODUCT_NAME__')
    await module.default()
    status.value = 'WASM module loaded. Attempting auto-activation...'

    // The WASM SDK will fetch the license from __NAMESPACE__/license.json automatically.
    activateFromLicenseFile()
    status.value = 'License check initiated — open the browser console to see the result.'
  } catch (e: any) {
    status.value = `Auto-activation failed: ${e.message}`
  }
})
</script>

<template>
  <section class="max-w-xl mx-auto text-center p-6 border border-gray-200 dark:border-gray-700 rounded-xl bg-gray-50 dark:bg-gray-800/50">
    <h2 class="text-xl font-semibold text-gray-800 dark:text-gray-200 mb-2">Auto-load License</h2>
    <p class="text-gray-500 dark:text-gray-400 text-sm mb-3">
      This component loads the license automatically from
      <code class="bg-gray-200 dark:bg-gray-700 text-gray-800 dark:text-gray-200 px-1.5 py-0.5 rounded text-xs font-mono">public/__NAMESPACE__/license.json</code>.
      Place your license file there and the WASM SDK will find it.
    </p>
    <p class="text-gray-500 dark:text-gray-400 italic">{{ status }}</p>
    <div id="__PRODUCT_NAME__-auto-app"></div>
  </section>
</template>
