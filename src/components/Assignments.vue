<script setup>

import {computed, onBeforeMount, ref} from "vue";
import AssignmentList from "@/components/AssignmentList.vue";
import AssignmentCreate from "@/components/AssignmentCreate.vue";

// const lists = ref([
//   { name: 'Read documentation', complete: false, id: 1, tag: 'Vue' },
//   { name: 'Practice topics', complete: false, id: 2, tag: 'Docker' },
//   { name: 'Watch tutorial', complete: false, id: 3, tag: 'Vue' },
//   { name: 'Make projects', complete: false, id: 4, tag: 'JS' },
// ])

const lists = ref([])
const show = ref(true)

onBeforeMount(async () => {
  try {
    const response = await fetch('http://localhost:5175/assignments');
    lists.value = await response.json()
  } catch (error) {
    console.error('Error fetching assignments:', error);
  }
});

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
  <div class="flex gap-10">
    <AssignmentList :lists="inCompleteAssignment" title="In Complete">
      <assignment-create @addedAssignment="addAssignment"/>
    </AssignmentList>
    <br>
    <AssignmentList
        v-if="show"
        :lists="completeAssignment"
        title="Completed"
        cross
        @hide="show = false"
    />
    <br>
  </div>

</template>
