<script setup>
import { ref } from 'vue';

const props = defineProps({
  options: Array,
  placeholder: String,
  value: Object
});

const isDropDownOpen = ref(false);
const selectedOption = ref(props.value);
const emit = defineEmits(['update:value']);

const openDropDown = () => {
  isDropDownOpen.value = !isDropDownOpen.value;
};

const handleSelect = (option) => {
  selectedOption.value = option;
  isDropDownOpen.value = false;
  emit('update:value', option);
};
</script>

<template>
  <div class="relative hover:cursor-pointer w-80">
    <div
      @click="openDropDown"
      class="flex items-center justify-between border-2 rounded-t-lg p-2.5"
      :class="{ 'rounded-b-lg': !isDropDownOpen }"
    >
      <span class="text-xl truncate" :class="{ 'text-slate-400': !selectedOption }">
        {{ selectedOption ? selectedOption.label : props.placeholder }}
      </span>
      <svg
        class="w-6 transition-transform duration-300 m-l-2.5"
        :class="{ 'rotate-180': isDropDownOpen }"
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        strokeWidth="{1.5}"
        stroke="currentColor"
        className="w-6 h-6"
      >
        <path strokeLinecap="round" strokeLinejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
      </svg>
    </div>
    <Transition>
      <div
        class="absolute bg-white shadow-2xl w-full border-2 border-t-0 rounded-b-lg"
        v-show="isDropDownOpen"
      >
        <div
          class="p-2 hover:bg-slate-100"
          v-for="(option, id) in props.options"
          :key="id"
          @click="handleSelect(option)"
        >
          {{ option.label }}
        </div>
      </div>
    </Transition>
  </div>
</template>

<style>
/* Styles for Vue animation */
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
