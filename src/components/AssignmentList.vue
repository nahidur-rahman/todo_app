<script setup>
import {computed, ref} from "vue";
import AssignmentTag from "@/components/AssignmentTag.vue";

const props = defineProps({
  lists: Array,
  allList: Array,
  title: String,
})

const currentTag = ref('All')
console.log(props.allList)

const filterAssignment = computed(() => {
  if (currentTag.value === 'All') {
    return props.lists
  }
  return props.lists.filter(list => list.tag === currentTag.value)
})
console.log(filterAssignment)
const tags = computed(() => {
  return [ 'All', ...new Set(props.lists.map(a => a.tag))]
})
</script>

<template>
  <section v-if="props.lists.length" class="bg-gray-300 border rounded px-4 py-4">
    <h3 class="font-bold mb-3">{{ props.title }} Assignment ({{ props.lists.length }})</h3>

    <assignment-tag
        v-model:currentTag="currentTag"
        :tags="tags"
    />
    <ul>
      <li
          v-for="list in filterAssignment"
          :key="list.id"
      >
          <label class="p-2 flex justify-between">
            {{ list.name }}
            <input type="checkbox" v-model="list.complete">
          </label>
        </li>
    </ul>
  </section>

</template>