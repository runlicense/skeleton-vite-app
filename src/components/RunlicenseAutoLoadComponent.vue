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
  <section class="max-w-xl mx-auto text-center p-5 border border-gray-200 dark:border-gray-700 rounded-lg">
    <p class="text-gray-500 dark:text-gray-400 text-sm mb-3">
      Place your license file at
      <code class="text-gray-700 dark:text-gray-300 text-xs font-mono">public/__NAMESPACE__/license.json</code>
      and the WASM SDK will find it.
    </p>
    <p class="text-gray-400 dark:text-gray-500 text-sm">{{ status }}</p>
    <div id="__PRODUCT_NAME__-auto-app"></div>
  </section>
</template>
