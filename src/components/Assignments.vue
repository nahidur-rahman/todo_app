<script setup>

import {computed, ref} from "vue";
import AssignmentList from "@/components/AssignmentList.vue";
import AssignmentCreate from "@/components/AssignmentCreate.vue";

const lists = ref([
  { name: 'Read documentation', complete: false, id: 1, tag: 'Vue' },
  { name: 'Practice topics', complete: false, id: 2, tag: 'Docker' },
  { name: 'Watch tutorial', complete: false, id: 3, tag: 'Vue' },
  { name: 'Make projects', complete: false, id: 4, tag: 'JS' },
])

function addAssignment(name) {
  if (name.length > 0) {
    const newList = {
      name: name,
      complete: false,
      id: lists.value.length + 1
    }
    lists.value.push(newList)
  }
}

const completeAssignment = computed(() => {
  return lists.value.filter(list => list.complete)
})
const inCompleteAssignment = computed(() => {
  return lists.value.filter(list => !list.complete)
})

</script>

<template>

  <AssignmentList :lists="inCompleteAssignment" title="In Complete" :allList="lists"/><br>
  <AssignmentList :lists="completeAssignment" title="Completed" /><br>

  <assignment-create class="" @addedAssignment="addAssignment"/>

</template>
