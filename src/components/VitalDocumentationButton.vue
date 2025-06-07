<template>
  <VitalDocumentation
    title="VitalButton"
    description="Cette page présente toutes les variations du composant individuel VitalButton."
  >
    <section class="vital-documentation-section">
      <h2>Variantes (Colors)</h2>
      <div class="flex">
        <VitalButton variant="primary" @click="handleButtonClick('Primaire')"
          >Primaire</VitalButton
        >
        <VitalButton
          variant="secondary"
          @click="handleButtonClick('Secondaire')"
          >Secondaire</VitalButton
        >
        <VitalButton variant="danger" @click="handleButtonClick('Danger')"
          >Danger</VitalButton
        >
      </div>
    </section>

    <section class="vital-documentation-section">
      <h2>Tailles (Sizes)</h2>
      <div class="flex">
        <VitalButton size="small" @click="handleButtonClick('Petit')"
          >Petit</VitalButton
        >
        <VitalButton size="medium" @click="handleButtonClick('Moyen')"
          >Moyen</VitalButton
        >
        <VitalButton size="large" @click="handleButtonClick('Grand')"
          >Grand</VitalButton
        >
      </div>
    </section>

    <section class="vital-documentation-section">
      <h2>État Désactivé (Disabled)</h2>
      <div class="flex">
        <VitalButton variant="primary" :disabled="true">Désactivé</VitalButton>
        <VitalButton variant="secondary" :disabled="true"
          >Désactivé</VitalButton
        >
        <VitalButton variant="danger" :disabled="true">Désactivé</VitalButton>
      </div>
    </section>
  </VitalDocumentation>
</template>

<script setup>
import VitalDocumentation from './VitalDocumentation.vue';
import VitalButton from './VitalButton.vue';

function handleButtonClick(buttonName) {
  alert(`Bouton "${buttonName}" cliqué !`);
}
</script>

<style scoped>
.flex {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
}
</style>
