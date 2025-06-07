<template>
  <VitalDocumentation
    title="VitalSelect"
    description="Un composant de sélection déroulante (dropdown) moderne, personnalisable et entièrement accessible."
  >
    <section class="vital-documentation-section">
      <h2>Exemple de base (Sélection unique)</h2>
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
      <h2>Sélection Multiple</h2>
      <p class="vital-documentation-description">
        En ajoutant la propriété <code>multiple</code>, l'utilisateur peut
        sélectionner plusieurs valeurs. Le <code>v-model</code> doit être lié à
        un tableau (Array). Une barre de recherche et des actions rapides sont
        aussi disponibles.
      </p>
      <div class="flex">
        <VitalSelect
          v-model="selectedTools"
          :options="toolOptions"
          placeholder="Choisissez vos outils"
          :multiple="true"
        />
      </div>
      <p class="result">
        Valeurs sélectionnées :
        <strong>{{ selectedTools.join(', ') || 'Aucune' }}</strong>
      </p>
    </section>

    <section class="vital-documentation-section">
      <h2>État Désactivé (Disabled)</h2>
      <p class="vital-documentation-description">
        Avec la propriété <code>disabled: true</code>, le composant n'est plus
        interactif. Cela fonctionne pour les sélections uniques et multiples.
      </p>
      <div class="flex">
        <VitalSelect
          v-model="preselectedLanguage"
          :options="languageOptions"
          :disabled="true"
        />
        <VitalSelect
          v-model="selectedToolsDisabled"
          :options="toolOptions"
          placeholder="Sélection multiple désactivée"
          :disabled="true"
          :multiple="true"
        />
      </div>
    </section>
  </VitalDocumentation>
</template>

<script setup>
import { ref } from 'vue';

import VitalDocumentation from '../components/VitalDocumentation.vue';
import VitalSelect from '../components/VitalSelect.vue';
import VitalButton from '../components/VitalButton.vue';

// --- Sélection Unique ---
const selectedFramework = ref(null);
const frameworkOptions = ref([
  { value: 'vue', text: 'Vue.js' },
  { value: 'react', text: 'React' },
  { value: 'angular', text: 'Angular' },
  { value: 'svelte', text: 'Svelte' },
  { value: 'solid', text: 'Solid.js' },
]);

const preselectedLanguage = ref('js');
const languageOptions = ref([
  { value: 'js', text: 'JavaScript' },
  { value: 'ts', text: 'TypeScript' },
  { value: 'python', text: 'Python' },
]);

// --- Sélection Multiple ---
const selectedTools = ref(['vite', 'pinia']);
const toolOptions = ref([
    { value: 'vite', text: 'Vite' },
    { value: 'pinia', text: 'Pinia' },
    { value: 'vue-router', text: 'Vue Router' },
    { value: 'vitest', text: 'Vitest' },
    { value: 'storybook', text: 'Storybook' },
    { value: 'eslint', text: 'ESLint' },
    { value: 'prettier', text: 'Prettier' },
]);

const selectedToolsDisabled = ref(['vite']);

</script>

<style scoped>
.result {
  margin-top: 1rem;
  background-color: #f8f9fa;
  padding: 0.75rem;
  border-radius: 6px;
  border: 1px solid #e9ecef;
  font-size: 0.9rem;
  word-wrap: break-word;
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
  flex-wrap: wrap;
}
</style>
