<script setup>

import Assignment from "@/components/Assignment.vue";
import {computed, ref} from "vue";

const props = defineProps({
  assignments: Array,
  title: String,
})

const currentTag = ref('all');

const tags = computed(() => {
  return ['all', ...new Set(props.assignments.map(a => a.tag))];
});

const filteredAssignments = computed(() => {
  if(currentTag.value === 'all') {
    return props.assignments
  }

  return props.assignments.filter(a => a.tag === currentTag.value)
});
</script>

<template>
    <section v-show="assignments.length">
      <h2 class="font-bold mb-2">
        {{ title }}
        <span>({{assignments.length}})</span>

        <div class="flex gap-2 mt-2">
          <button
              @click="currentTag = tag"
              v-for="tag in tags"
              class="border rounded px-1 py-px text-xs"
              :class="{
                'border-blue-500 text-blue-500': tag === currentTag
              }"
          >{{tag}}</button>
        </div>
      </h2>

      <ul class="border border-gray-600 divide-y divide-gray-600 mt-4">
        <Assignment
          v-for="assignment in filteredAssignments"
          :key="assignment"
          :assignment="assignment"
        />
      </ul>

    </section>
</template>

<style>
</style>
