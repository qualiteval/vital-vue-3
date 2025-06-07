<template>
  <button :class="buttonClasses" :disabled="disabled" @click="handleClick">
    <slot></slot>
  </button>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  variant: {
    type: String,
    default: 'primary',
    validator: (value) => ['primary', 'secondary', 'danger'].includes(value),
  },
  size: {
    type: String,
    default: 'medium',
    validator: (value) => ['small', 'medium', 'large'].includes(value),
  },
  disabled: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(['click']);

const buttonClasses = computed(() => {
  return [
    `vital-button`,
    `${props.variant}`,
    `${props.size}`,
    { disabled: props.disabled },
  ];
});

function handleClick(event) {
  if (!props.disabled) {
    emit('click', event);
  }
}
</script>

<style scoped>
.vital-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border: 1px solid transparent;
  border-radius: 8px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica,
    Arial, sans-serif;
  font-weight: 600;
  cursor: pointer;
  outline: none;
  transition: all 0.2s ease-in-out;
  user-select: none;
  white-space: nowrap;
}
.vital-button:focus-visible {
  box-shadow: 0 0 0 3px rgba(66, 153, 225, 0.6);
}
.vital-button.primary {
  background-color: #42b983;
  color: white;
}
.vital-button.primary:hover {
  background-color: #38a170;
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}
.vital-button.primary:active {
  transform: translateY(0);
  box-shadow: none;
}
.vital-button.secondary {
  background-color: #f0f2f5;
  color: #333;
  border-color: #dcdfe6;
}
.vital-button.secondary:hover {
  background-color: #e4e7ed;
  border-color: #c8cdd4;
  transform: translateY(-1px);
}
.vital-button.secondary:active {
  transform: translateY(0);
}
.vital-button.danger {
  background-color: #e53e3e;
  color: white;
}
.vital-button.danger:hover {
  background-color: #c53030;
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(229, 62, 62, 0.2);
}
.vital-button.danger:active {
  transform: translateY(0);
  box-shadow: none;
}
.vital-button.small {
  padding: 0.5rem 0.75rem;
  font-size: 0.875rem;
}
.vital-button.medium {
  padding: 0.75rem 1.25rem;
  font-size: 1rem;
}
.vital-button.large {
  padding: 1rem 1.75rem;
  font-size: 1.125rem;
}
.vital-button.disabled {
  opacity: 0.6;
  cursor: not-allowed;
  transform: none;
  box-shadow: none;
}
.vital-button.disabled:hover {
  transform: none;
}
</style>
