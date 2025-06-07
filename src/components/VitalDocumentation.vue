<template>
  <div class="vital-documentation-layout">
    <header class="vital-documentation-header">
      <h1>{{ title }}</h1>
      <p v-if="description">{{ description }}</p>
    </header>
    <main class="vital-documentation-content">
      <slot></slot>
    </main>
  </div>
</template>

<script setup>
defineProps({
  title: {
    type: String,
    required: true,
  },
  description: {
    type: String,
    default: '',
  },
});
</script>

<style scoped>
.vital-documentation-layout {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica,
    Arial, sans-serif;
  max-width: 800px;
  margin: 2rem auto;
  padding: 2rem;
  background-color: #fdfdff;
  border: 1px solid #eef;
  border-radius: 12px;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.05);
  color: #343a40;
}
.vital-documentation-header {
  text-align: center;
  border-bottom: 1px solid #e9ecef;
  padding-bottom: 1.5rem;
  margin-bottom: 2rem;
}
.vital-documentation-header h1 {
  font-size: 2rem;
  font-weight: 700;
  color: #212529;
}
.vital-documentation-header p {
  font-size: 1.1rem;
  color: #6c757d;
  margin-top: 0.5rem;
}
.vital-documentation-content:deep(.vital-documentation-section) {
  margin-bottom: 2.5rem;
}
.vital-documentation-content:deep(.vital-documentation-section h2) {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #495057;
  padding-bottom: 0.5rem;
  border-bottom: 1px solid #dee2e6;
}
.vital-documentation-content:deep(.vital-documentation-description) {
  margin-bottom: 1rem;
  color: #6c757d;
  line-height: 1.6;
}
.vital-documentation-content:deep(code) {
  background-color: #e9ecef;
  padding: 0.2em 0.4em;
  border-radius: 4px;
  color: #c7254e;
  font-size: 0.9em;
}
</style>
