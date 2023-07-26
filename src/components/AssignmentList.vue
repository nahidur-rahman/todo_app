<script setup>
import {computed, ref} from "vue";
import AssignmentTag from "@/components/AssignmentTag.vue";

const props = defineProps({
  lists: Array,
  title: String,
  cross: { type: Boolean, default: false}
})

const currentTag = ref('All')
// const show = ref(true)

const filterAssignment = computed(() => {
  if (currentTag.value === 'All') {
    return props.lists
  }
  return props.lists.filter(list => list.tag === currentTag.value)
})

const tags = computed(() => {
  return [ 'All', ...new Set(props.lists.map(a => a.tag))]
})
</script>

<template>
  <section v-if="props.lists.length" class="bg-gray-300 border rounded px-4 py-4 w-80">
    <div class="flex justify-between items-start">
      <h3
          class="font-bold mb-3"
      >
        {{ props.title }} Assignment ({{ props.lists.length }})
      </h3>

      <button
          class="text-2xl mb-2"
          v-show="cross"
          @click="$emit('hide')"
      >
        &times;
      </button>
    </div>


    <assignment-tag
        v-model:currentTag="currentTag"
        :tags="tags"
        class="mb-2"
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
    <slot/>
  </section>

</template>