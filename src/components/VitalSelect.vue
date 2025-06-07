<template>
  <div :class="{ disabled: disabled }" ref="selectRef" class="vital-select">
    <button
      class="vital-select-trigger"
      @click="toggleDropdown"
      :disabled="disabled"
      aria-haspopup="listbox"
      :aria-expanded="isOpen"
    >
      <span v-if="modelValue">{{ selectedOptionText }}</span>
      <span v-else class="vital-select-placeholder">{{ placeholder }}</span>

      <svg
        class="vital-select-chevron"
        :class="{ 'vital-select-chevron--open': isOpen }"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 20 20"
        fill="currentColor"
      >
        <path
          fill-rule="evenodd"
          d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
          clip-rule="evenodd"
        />
      </svg>
    </button>

    <transition name="fade">
      <ul v-if="isOpen" class="vital-select-options" role="listbox">
        <li
          v-for="option in options"
          :key="option.value"
          class="vital-select-option"
          :class="{
            'vital-select-option--selected': modelValue === option.value,
          }"
          @click="selectOption(option)"
          role="option"
          :aria-selected="modelValue === option.value"
        >
          {{ option.text }}
        </li>
      </ul>
    </transition>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';

const props = defineProps({
  modelValue: {
    type: [String, Number],
    default: null,
  },
  options: {
    type: Array,
    default: () => [],
    validator: (opts) => opts.every((opt) => 'value' in opt && 'text' in opt),
  },
  placeholder: {
    type: String,
    default: 'Sélectionnez une option',
  },
  disabled: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(['update:modelValue']);

const isOpen = ref(false);
const selectRef = ref(null);

const selectedOptionText = computed(() => {
  const selected = props.options.find((opt) => opt.value === props.modelValue);
  return selected ? selected.text : props.placeholder;
});

function toggleDropdown() {
  if (!props.disabled) {
    isOpen.value = !isOpen.value;
  }
}

function selectOption(option) {
  emit('update:modelValue', option.value);
  isOpen.value = false;
}

function handleClickOutside(event) {
  if (selectRef.value && !selectRef.value.contains(event.target)) {
    isOpen.value = false;
  }
}

onMounted(() => {
  document.addEventListener('click', handleClickOutside);
});

onUnmounted(() => {
  document.removeEventListener('click', handleClickOutside);
});
</script>

<style scoped>
.vital-select {
  position: relative;
  width: 240px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica,
    Arial, sans-serif;
}
.vital-select-trigger {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 0.6rem 0.9rem;
  background-color: white;
  border: 1px solid #dcdfe6;
  border-radius: 8px;
  cursor: pointer;
  text-align: left;
  transition: border-color 0.2s, box-shadow 0.2s;
}
.vital-select-trigger:focus,
.vital-select-trigger:focus-visible {
  outline: none;
  border-color: #42b983;
  box-shadow: 0 0 0 3px rgba(66, 185, 131, 0.3);
}
.vital-select-placeholder {
  color: #a8abb2;
}
.vital-select-chevron {
  width: 20px;
  height: 20px;
  color: #909399;
  transition: transform 0.2s ease-in-out;
}
.vital-select-chevron--open {
  transform: rotate(180deg);
}
.vital-select-options {
  position: absolute;
  top: calc(100% + 4px);
  left: 0;
  width: 100%;
  margin: 0;
  padding: 0.5rem 0;
  list-style: none;
  background-color: white;
  border: 1px solid #e4e7ed;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  z-index: 10;
  max-height: 200px;
  overflow-y: auto;
}
.vital-select-option {
  padding: 0.6rem 0.9rem;
  cursor: pointer;
  transition: background-color 0.2s;
}
.vital-select-option:hover {
  background-color: #f5f7fa;
}
.vital-select-option--selected {
  color: #42b983;
  font-weight: 600;
  background-color: #f0fdf4;
}
.vital-select.disabled .vital-select-trigger {
  background-color: #f5f7fa;
  cursor: not-allowed;
  color: #c0c4cc;
}
.vital-select.disabled .vital-select-placeholder {
  color: #c0c4cc;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.15s ease, transform 0.15s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(-5px);
}
</style>
