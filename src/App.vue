<script setup lang="ts">
import RunlicensePasteInputComponent from './components/RunlicensePasteInputComponent.vue'
import RunlicenseAutoLoadComponent from './components/RunlicenseAutoLoadComponent.vue'
</script>

<template>
  <div class="app">
    <header>
      <h1>__PRODUCT_NAME__</h1>
      <p class="subtitle">RunLicense Demo App</p>
    </header>

    <div class="examples">
      <div class="example">
        <h3>Method 1: Paste License</h3>
        <p class="method-description">Manually paste a license JSON string to activate.</p>
        <RunlicensePasteInputComponent />
      </div>

      <hr />

      <div class="example">
        <h3>Method 2: Auto-load License</h3>
        <p class="method-description">
          License is loaded automatically from
          <code>public/__NAMESPACE__/license.json</code>.
        </p>
        <RunlicenseAutoLoadComponent />
      </div>
    </div>
  </div>
</template>

<style scoped>
.app {
  max-width: 720px;
  margin: 0 auto;
  padding: 2rem 1rem;
  font-family: system-ui, sans-serif;
}

header {
  text-align: center;
  margin-bottom: 2.5rem;
}

header h1 {
  font-size: 2.5rem;
  margin-bottom: 0.25rem;
}

.subtitle {
  color: #888;
  font-size: 1.1rem;
}

.examples {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.example h3 {
  text-align: center;
  font-size: 1.2rem;
  margin-bottom: 0.25rem;
}

.method-description {
  text-align: center;
  color: #666;
  font-size: 0.9rem;
  margin-bottom: 1rem;
}

.method-description code {
  background: #e5e7eb;
  padding: 0.15rem 0.4rem;
  border-radius: 3px;
  font-size: 0.85rem;
}

hr {
  border: none;
  border-top: 1px solid #e5e7eb;
  margin: 1rem 0;
}
</style>
