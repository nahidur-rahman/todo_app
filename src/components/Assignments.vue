<script setup>

import { computed, defineProps, defineEmits, ref } from "vue";
import AssignmentList from "@/components/AssignmentList.vue";
import AssignmentCreate from "@/components/AssignmentCreate.vue";

const props = defineProps({
lists: Array,
tags: Array
// addAssignment: Function
})

const completeAssignment = computed(() => {
return props.lists.filter(list => list.complete)
})
const inCompleteAssignment = computed(() => {
return props.lists.filter(list => ! list.complete)
})

const emit = defineEmits(['addAssignment']);

const newAssignment = ref('');

const addAssignment = (newAssignment) => {
emit('addAssignment', newAssignment);
// newAssignment.value = "";
//   props.lists.value.push(newAssignment);
};
</script>

<template>
  <AssignmentList :lists="inCompleteAssignment" title="In Complete" :tags=tags :allList="lists"/>
  <br>
  <AssignmentList :lists="completeAssignment" title="Completed"/><br>

    <assignment-create @addAssignment="addAssignment"/>
<!--  <form @submit.prevent="addAssignment" class="justify-between">-->
<!--    <div class="border border-gray-200 mx-2 flex justify-between">-->
<!--      <input placeholder="New assignment" v-model="newAssignment">-->
<!--      <button type="submit" class="p-1 px-3 bg-gray-100 place-items-center">Add</button>-->
<!--    </div>-->
<!--  </form>-->

</template>
