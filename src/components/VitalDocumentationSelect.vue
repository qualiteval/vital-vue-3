<template>
  <VitalDocumentation
    title="VitalSelect"
    description="Un composant de sélection déroulante (dropdown) moderne, personnalisable et entièrement accessible."
  >
    <section class="vital-documentation-section">
      <h2>Exemple de base</h2>
      <p class="vital-documentation-description">
        Utilisation standard du composant avec un <code>v-model</code> pour lier
        la valeur sélectionnée.
      </p>
      <div class="flex">
        <VitalSelect
          v-model="selectedFramework"
          :options="frameworkOptions"
          placeholder="Choisissez un framework"
        />
      </div>
      <p class="result">
        Valeur sélectionnée :
        <strong>{{ selectedFramework || 'Aucune' }}</strong>
      </p>
    </section>

    <section class="vital-documentation-section">
      <h2>Valeur pré-sélectionnée</h2>
      <p class="vital-documentation-description">
        Le composant affiche correctement la valeur initiale définie dans le
        script.
      </p>
      <div class="flex">
        <VitalSelect v-model="preselectedLanguage" :options="languageOptions" />
      </div>
      <p class="result">
        Valeur initiale : <strong>{{ preselectedLanguage }}</strong>
      </p>
    </section>

    <section class="vital-documentation-section">
      <h2>État Désactivé (Disabled)</h2>
      <p class="vital-documentation-description">
        Avec la propriété <code>disabled: true</code>, le composant n'est plus
        interactif.
      </p>
      <div class="flex">
        <VitalSelect
          v-model="preselectedLanguage"
          :options="languageOptions"
          :disabled="true"
        />
        <VitalSelect
          :options="languageOptions"
          placeholder="Aussi désactivé"
          :disabled="true"
        />
      </div>
    </section>
  </VitalDocumentation>
</template>

<script setup>
import { ref } from 'vue';

import VitalDocumentation from './VitalDocumentation.vue';
import VitalSelect from './VitalSelect.vue';

const selectedFramework = ref(null);
const frameworkOptions = ref([
  { value: 'vue', text: 'Vue.js' },
  { value: 'react', text: 'React' },
  { value: 'angular', text: 'Angular' },
  { value: 'svelte', text: 'Svelte' },
]);

const preselectedLanguage = ref('js');
const languageOptions = ref([
  { value: 'js', text: 'JavaScript' },
  { value: 'ts', text: 'TypeScript' },
  { value: 'python', text: 'Python' },
]);
</script>

<style scoped>
.result {
  margin-top: 1rem;
  background-color: #f8f9fa;
  padding: 0.75rem;
  border-radius: 6px;
  border: 1px solid #e9ecef;
  font-size: 0.9rem;
}
.result strong {
  color: #42b983;
}
.flex {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
}
</style>
