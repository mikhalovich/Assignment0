<script setup>
import DropDownSelect from './components/DropDownSelect.vue';

import { reactive } from 'vue';

const dropDownOptions = reactive([
  { label: 'Very long option 1 for selecttor to show truncate', value: 'option1' },
  { label: 'Option 2 for select', value: 'option2' },
  { label: 'Option 3 for select', value: 'option3' }
]);
</script>

<template>
  <main>
    <h2 class="text-3xl mb-4">Dop down selector</h2>
    <DropDownSelect v-model="selectedOption" :options="dropDownOptions" placeholder="Select..." />
  </main>
</template>
