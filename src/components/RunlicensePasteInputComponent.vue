<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { activateFromLicenseString } from '__PRODUCT_NAME__'

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
    activateFromLicenseString(licenseString.value)
    status.value = 'License check initiated — open the browser console to see the result.'
  } catch (e: any) {
    status.value = `Activation failed: ${e.message}`
  }
}
</script>

<template>
  <section class="max-w-xl mx-auto text-center">
    <p class="text-gray-400 dark:text-gray-500 text-sm mb-4">{{ status }}</p>

    <div v-if="isReady" class="flex flex-col gap-3 mb-6">
      <textarea
        v-model="licenseString"
        placeholder="Paste your license JSON here..."
        rows="6"
        class="w-full px-3 py-3 border border-gray-200 dark:border-gray-700 rounded-lg font-mono text-sm bg-white dark:bg-gray-800 text-gray-900 dark:text-gray-100 placeholder-gray-300 dark:placeholder-gray-600 resize-y focus:outline-none focus:ring-1 focus:ring-gray-300 dark:focus:ring-gray-600 focus:border-gray-300 dark:focus:border-gray-600"
      ></textarea>
      <button
        @click="handleActivate"
        :disabled="!licenseString"
        class="px-5 py-2.5 bg-gray-900 dark:bg-gray-100 text-white dark:text-gray-900 text-sm font-medium rounded-lg transition-colors duration-150 hover:bg-gray-800 dark:hover:bg-gray-200 disabled:bg-gray-200 dark:disabled:bg-gray-700 disabled:text-gray-400 dark:disabled:text-gray-500 disabled:cursor-not-allowed"
      >
        Activate License
      </button>
    </div>

    <div id="__PRODUCT_NAME__-app"></div>
  </section>
</template>
