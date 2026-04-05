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
    <p class="text-gray-500 dark:text-gray-400 italic mb-4">{{ status }}</p>

    <div v-if="isReady" class="flex flex-col gap-3 mb-6">
      <textarea
        v-model="licenseString"
        placeholder="Paste your license JSON here..."
        rows="6"
        class="w-full px-3 py-3 border border-gray-300 dark:border-gray-600 rounded-lg font-mono text-sm bg-white dark:bg-gray-800 text-gray-900 dark:text-gray-100 placeholder-gray-400 dark:placeholder-gray-500 resize-y focus:outline-none focus:ring-2 focus:ring-accent focus:border-transparent"
      ></textarea>
      <button
        @click="handleActivate"
        :disabled="!licenseString"
        class="px-6 py-3 bg-accent text-white font-medium rounded-lg transition-all duration-200 hover:brightness-110 hover:shadow-md disabled:bg-gray-300 dark:disabled:bg-gray-600 disabled:cursor-not-allowed disabled:shadow-none"
      >
        Activate License
      </button>
    </div>

    <div id="__PRODUCT_NAME__-app"></div>
  </section>
</template>
