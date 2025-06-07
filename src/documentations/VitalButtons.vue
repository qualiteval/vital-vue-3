<template>
  <VitalDocumentation
    title="VitalButtons"
    description="Cette page de démonstration présente le composant VitalButtons pour grouper des VitalButton."
  >
    <section class="vital-documentation-section">
      <h2>Groupe de boutons standard</h2>
      <p class="vital-documentation-description">
        Par défaut, les boutons ont un espacement entre eux pour une séparation
        claire.
      </p>
      <VitalButtons>
        <VitalButton variant="primary" @click="handleButtonClick('Profil')"
          >Profil</VitalButton
        >
        <VitalButton variant="secondary" @click="handleButtonClick('Réglages')"
          >Réglages</VitalButton
        >
        <VitalButton variant="danger" @click="handleButtonClick('Déconnexion')"
          >Déconnexion</VitalButton
        >
      </VitalButtons>
    </section>

    <section class="vital-documentation-section">
      <h2>Groupe de boutons "attaché"</h2>
      <p class="vital-documentation-description">
        Avec la propriété <code>attached: true</code>, les boutons sont collés
        pour former un bloc unifié.
      </p>
      <VitalButtons attached>
        <VitalButton variant="secondary" @click="handleButtonClick('Gauche')"
          >Gauche</VitalButton
        >
        <VitalButton variant="secondary" @click="handleButtonClick('Centre')"
          >Centre</VitalButton
        >
        <VitalButton variant="secondary" @click="handleButtonClick('Droite')"
          >Droite</VitalButton
        >
      </VitalButtons>
    </section>
  </VitalDocumentation>
</template>

<script setup>
import VitalDocumentation from '../components/VitalDocumentation.vue';
import VitalButton from '../components/VitalButton.vue';
import VitalButtons from '../components/VitalButtons.vue';

function handleButtonClick(buttonName) {
  alert(`Action : "${buttonName}"`);
}
</script>
