<script setup lang="ts">
import RunlicensePasteInputComponent from './components/RunlicensePasteInputComponent.vue'
import RunlicenseAutoLoadComponent from './components/RunlicenseAutoLoadComponent.vue'
import {ref} from "vue";

const showingMethod = ref(1);
</script>

<template>
  <div class="max-w-2xl mx-auto px-6 py-12 font-sans min-h-screen">
    <header class="text-center mb-10">
      <h1 class="text-3xl font-semibold tracking-tight text-gray-900 dark:text-gray-100">__PRODUCT_NAME__</h1>
      <p class="text-gray-400 dark:text-gray-500 text-sm mt-1">RunLicense Demo App</p>
      <p class="mt-4 px-3 py-1.5 text-gray-500 dark:text-gray-400 text-xs rounded border border-gray-200 dark:border-gray-700 inline-block">
        Open browser console <kbd class="px-1 py-0.5 bg-gray-100 dark:bg-gray-700 rounded text-xs font-mono">F12</kbd> to see validation output
      </p>
    </header>

    <div class="mb-8">
      <div class="flex border border-gray-200 dark:border-gray-700 rounded-lg overflow-hidden">
        <button
          @click="showingMethod = 1"
          :class="[
            'flex-1 px-4 py-2.5 text-sm font-medium transition-colors duration-150',
            showingMethod === 1
              ? 'bg-gray-900 dark:bg-gray-100 text-white dark:text-gray-900'
              : 'bg-white dark:bg-gray-800 text-gray-500 dark:text-gray-400 hover:text-gray-700 dark:hover:text-gray-200 hover:bg-gray-50 dark:hover:bg-gray-750'
          ]"
        >
          Paste License
        </button>
        <button
          @click="showingMethod = 2"
          :class="[
            'flex-1 px-4 py-2.5 text-sm font-medium transition-colors duration-150 border-l border-gray-200 dark:border-gray-700',
            showingMethod === 2
              ? 'bg-gray-900 dark:bg-gray-100 text-white dark:text-gray-900'
              : 'bg-white dark:bg-gray-800 text-gray-500 dark:text-gray-400 hover:text-gray-700 dark:hover:text-gray-200 hover:bg-gray-50 dark:hover:bg-gray-750'
          ]"
        >
          Reference License File
        </button>
      </div>
    </div>

    <div>
      <div v-if="showingMethod === 1">
        <p class="text-center text-gray-500 dark:text-gray-400 text-sm mb-5">Paste a license JSON string to activate.</p>
        <RunlicensePasteInputComponent />
      </div>

      <div v-if="showingMethod === 2">
        <p class="text-center text-gray-500 dark:text-gray-400 text-sm mb-5">
          License is loaded automatically from
          <code class="text-gray-700 dark:text-gray-300 text-xs font-mono">public/__NAMESPACE__/license.json</code>
        </p>
        <RunlicenseAutoLoadComponent />
      </div>
    </div>

    <div class="mt-12 pt-6 border-t border-gray-100 dark:border-gray-800 text-center">
      <a
        href="https://runlicense.com/licenses/new"
        target="_blank"
        rel="noopener noreferrer"
        class="text-sm text-gray-400 dark:text-gray-500 hover:text-gray-600 dark:hover:text-gray-300 transition-colors duration-150"
      >
        Generate a new license &rarr;
      </a>
    </div>
  </div>
</template>
