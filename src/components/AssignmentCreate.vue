<script setup>
import {computed, ref} from "vue";

const props = defineProps({

})

const emits = defineEmits(['add']);

const newAssignment = ref('');
const add = () => {
  emits('add', newAssignment.value)

  newAssignment.value = ''
}
</script>

<template>
    <form @submit.prevent="add">
      <div class="border border-gray-600 text-black">
        <input v-model="newAssignment" placeholder="New assignment..." class="p-2">
        <button type="submit" class="bg-white p-2 border-l" >Add</button>
      </div>
    </form>
</template>

<style>

</style>
