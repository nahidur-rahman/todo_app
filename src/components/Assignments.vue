<script setup>

import {computed, defineProps, defineEmits} from "vue";
import AssignmentList from "@/components/AssignmentList.vue";
import AssignmentCreate from "@/components/AssignmentCreate.vue";

const props = defineProps({
  lists: Array,
  tags: Array
})

const completeAssignment = computed(() => {
  return props.lists.filter(list => list.complete)
})
const inCompleteAssignment = computed(() => {
  return props.lists.filter(list => !list.complete)
})

const emit = defineEmits(['addAssignment']);

const addAssignment = (newAssignment) => {
  emit('addAssignment', newAssignment);
};

</script>

<template>

  <AssignmentList :lists="inCompleteAssignment" title="In Complete" :tags=tags :allList="lists"/><br>
  <AssignmentList :lists="completeAssignment" title="Completed"/><br>

  <assignment-create @addAssignment="addAssignment"/>

</template>
