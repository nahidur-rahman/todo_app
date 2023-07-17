<script setup>
import {computed, ref} from 'vue'
import Assignments from "@/components/Assignments.vue";

const lists = ref([
  { name: 'Read documentation', complete: false, id: 1, tag: 'Vue' },
  { name: 'Practice topics', complete: false, id: 2, tag: 'Docker' },
  { name: 'Watch tutorial', complete: false, id: 3, tag: 'Vue' },
  { name: 'Make projects', complete: false, id: 4, tag: 'JS' },
])

// const tags = ref(['Math', 'Physics', 'Chemistry'])
const tags = computed(() => {
  return [ 'All', ...new Set(lists.value.map(a => a.tag))]
})


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
</script>

<template>
  <Assignments :lists="lists" :tags=tags @addAssignment="addAssignment"/>
</template>