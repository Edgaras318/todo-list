<script setup>
 import {ref} from "vue";

 const props = defineProps({
   type: {
     type: String,
     required: false,
     default: () => 'primary',
   },
   progressing: {
     type: Boolean,
     required: false,
     default: () => false,
   },
 })

</script>

<template>
 <button :class="{
      'border rounded px-5 py-2 disabled:cursor-not-allowed': true,
      'bg-blue-200 hover:bg-blue-400': type === 'primary',
      'bg-blue-600 hover:bg-blue-400 text-white': type === 'primary',
      'bg-purple-200 hover:bg-purple-400': type === 'secondary',
      'bg-gray-200 hover:bg-gray-400': type === 'muted',
      'loader': progressing,
      'loader': progressing,
    }" :disabled="progressing">
   <slot/>
 </button>
</template>

<style>

</style>
