<template>
  <div :class="groupClasses">
    <slot></slot>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  attached: {
    type: Boolean,
    default: false,
  },
});

const groupClasses = computed(() => {
  return ['vital-buttons', { attached: props.attached }];
});
</script>

<style scoped>
.vital-buttons {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
}
.vital-buttons.attached {
  gap: 0;
}
.vital-buttons.attached:deep(.vital-button) {
  border-radius: 0;
}
.vital-buttons.attached:deep(.vital-button:first-child) {
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
}
.vital-buttons.attached:deep(.vital-button:last-child) {
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
}
.vital-buttons.attached:deep(.vital-button:not(:first-child)) {
  margin-left: -1px;
}
.vital-buttons.attached:deep(.vital-button:focus-visible) {
  position: relative;
  z-index: 1;
}
</style>
