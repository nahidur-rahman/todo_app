<script setup>
import { ref } from 'vue'

const emit = defineEmits(['addedAssignment']);

const newAssignment = ref('');

const addAssignment = () => {
  emit('addedAssignment', newAssignment.value);
  newAssignment.value = "";
};
</script>

<template>

  <form @submit.prevent="addAssignment">
    <div class="border border-gray-500 mx-1 my-3 flex">
      <input class="flex-1" placeholder="New assignment..." v-model="newAssignment">
      <button type="submit" class="border border-gray-400 p-1 px-2 bg-green-300 place-items-center">Add</button>
    </div>
  </form>
</template>

