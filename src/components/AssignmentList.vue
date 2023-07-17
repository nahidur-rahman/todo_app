<script setup>
import {computed, defineProps, ref} from "vue";

const props = defineProps({
  lists: Array,
  allList: Array,
  title: String,
  tags: Array
})

const currentTag = ref('All')
console.log(props.allList)

const filterAssignment = computed(() => {
  if (currentTag.value === 'All') {
    return props.allList
  }
  return props.allList.filter(list => list.tag === currentTag.value)
})
console.log(filterAssignment)
// console.log(props.tags)
</script>

<template>
  <section v-if="props.lists.length" class="bg-gray-300 border rounded px-4 py-4">
    <h3 class="font-bold mb-3">{{ props.title }} Assignment ({{ props.lists.length }})</h3>

    <div class="flex gap-2">
      <button
          @click="currentTag = tag"
          v-for="tag in tags"
          class="bg-white border rounded px-1 py-px text-xs"
          :class="{
            'bg-blue-300' : tag === currentTag
          }"
      >
        {{ tag }}
      </button>
    </div>
    <!--    <ul>-->
    <!--      <li-->
    <!--          v-for="list in filterAssignment"-->
    <!--          :key="list.id"-->
    <!--      >-->
    <!--&lt;!&ndash;      <li-->
    <!--&lt;!&ndash;          v-for="list in props.lists"&ndash;&gt;-->
    <!--&lt;!&ndash;          :key="list.id"&ndash;&gt;-->
    <!--&lt;!&ndash;      >&ndash;&gt;&ndash;&gt;-->
    <!--        <label class="p-2 flex justify-between">-->
    <!--          {{ list.name }}-->
    <!--          <input type="checkbox" v-model="list.complete">-->
    <!--        </label>-->
    <!--      </li>-->
    <!--    </ul>-->
    <ul>
      <li
          v-for="list in filterAssignment"
          v-if="title === 'In Complete' && props.lists.includes(list)"
          :key="list.id"
      >
        <label class="p-2 flex justify-between">
          {{ list.name }}
          <input type="checkbox" v-model="list.complete">
        </label>
      </li>
      <li v-else v-for="list in props.lists" :key="list.id">
        <label class="p-2 flex justify-between">
          {{ list.name }}
          <input type="checkbox" v-model="list.complete">
        </label>
      </li>
    </ul>
  </section>

</template>