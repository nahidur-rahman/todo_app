<script setup>
const props = defineProps({
  tags: Array,
  currentTag: String
})
</script>

<template>
  <div class="flex gap-2">
    <button

        v-for="tag in tags"
        @click="$emit('update:currentTag', tag)"
        :class="[tag === props.currentTag ? 'bg-blue-300 border rounded px-1 py-px text-xs' : 'bg-white border rounded px-1 py-px text-xs']"
    >
      {{ tag }}
    </button>
  </div>
</template>
