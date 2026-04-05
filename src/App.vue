<script setup lang="ts">
import RunlicensePasteInputComponent from './components/RunlicensePasteInputComponent.vue'
import RunlicenseAutoLoadComponent from './components/RunlicenseAutoLoadComponent.vue'
import {ref} from "vue";

const showingMethod = ref(1);
</script>

<template>
  <div class="max-w-3xl mx-auto px-4 py-8 font-sans min-h-screen">
    <header class="text-center mb-10">
      <h1 class="text-4xl md:text-5xl font-bold tracking-tight text-gray-900 dark:text-gray-100">__PRODUCT_NAME__</h1>
      <p class="text-gray-500 dark:text-gray-400 text-lg mt-2">RunLicense Demo App</p>
      <p class="mt-3 px-4 py-2 bg-amber-50 dark:bg-amber-900/30 text-amber-700 dark:text-amber-300 text-sm rounded-lg border border-amber-200 dark:border-amber-700 inline-block">
        Open your browser console <kbd class="px-1.5 py-0.5 bg-amber-100 dark:bg-amber-800 rounded text-xs font-mono">F12</kbd> to see license validation output.
      </p>
    </header>

    <div class="bg-white dark:bg-gray-800/50 rounded-xl shadow-sm border border-gray-200 dark:border-gray-700 p-6 mb-8">
      <p class="text-sm font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wide mb-4">Activation Method</p>
      <div class="flex gap-3">
        <button
          @click="showingMethod = 1"
          :class="[
            'flex-1 px-4 py-2.5 rounded-lg text-sm font-medium transition-all duration-200',
            showingMethod === 1
              ? 'bg-accent text-white shadow-md'
              : 'bg-gray-100 dark:bg-gray-700 text-gray-600 dark:text-gray-300 hover:bg-gray-200 dark:hover:bg-gray-600'
          ]"
        >
          Paste License
        </button>
        <button
          @click="showingMethod = 2"
          :class="[
            'flex-1 px-4 py-2.5 rounded-lg text-sm font-medium transition-all duration-200',
            showingMethod === 2
              ? 'bg-accent text-white shadow-md'
              : 'bg-gray-100 dark:bg-gray-700 text-gray-600 dark:text-gray-300 hover:bg-gray-200 dark:hover:bg-gray-600'
          ]"
        >
          Reference License File
        </button>
      </div>
    </div>

    <div>
      <div v-if="showingMethod === 1">
        <h3 class="text-center text-lg font-semibold text-gray-800 dark:text-gray-200 mb-1">Method 1: Paste License</h3>
        <p class="text-center text-gray-500 dark:text-gray-400 text-sm mb-4">Manually paste a license JSON string to activate.</p>
        <RunlicensePasteInputComponent />
      </div>

      <div v-if="showingMethod === 2">
        <h3 class="text-center text-lg font-semibold text-gray-800 dark:text-gray-200 mb-1">Method 2: Auto-load License</h3>
        <p class="text-center text-gray-500 dark:text-gray-400 text-sm mb-4">
          License is loaded automatically from
          <code class="bg-gray-100 dark:bg-gray-700 text-gray-800 dark:text-gray-200 px-1.5 py-0.5 rounded text-xs font-mono">public/__NAMESPACE__/license.json</code>.
        </p>
        <RunlicenseAutoLoadComponent />
      </div>
    </div>

    <div class="mt-10 pt-8 border-t border-gray-200 dark:border-gray-700 text-center">
      <p class="text-sm text-gray-500 dark:text-gray-400 mb-4">Need a license for your project?</p>
      <a
        href="https://runlicense.com/licenses/new"
        target="_blank"
        rel="noopener noreferrer"
        class="inline-flex items-center gap-2 px-6 py-3 bg-accent text-white font-medium rounded-lg shadow-md hover:shadow-lg hover:brightness-110 transition-all duration-200"
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
          <path fill-rule="evenodd" d="M10 3a1 1 0 011 1v5h5a1 1 0 110 2h-5v5a1 1 0 11-2 0v-5H4a1 1 0 110-2h5V4a1 1 0 011-1z" clip-rule="evenodd" />
        </svg>
        Generate New License
      </a>
    </div>
  </div>
</template>
