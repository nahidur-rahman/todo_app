<script setup>
import { ref } from 'vue'

const emit = defineEmits(['addAssignment']);

const newAssignment = ref('');

const addAssignment = (event) => {
  emit('addAssignment', newAssignment.value);
  newAssignment.value = "";
};
</script>

<template>
  <form @submit.prevent="addAssignment">
    <div class="border border-gray-200 mx-2 my-2 flex justify-between">
      <input placeholder="New assignment" v-model="newAssignment">
      <button type="submit" class="p-1 px-2 bg-gray-100 place-items-center">Add</button>
    </div>
  </form>
</template>

