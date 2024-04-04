<script setup>
import {computed, ref, onMounted} from "vue";
import AssignmentList from "@/components/AssignmentList.vue";
import AssignmentCreate from "@/components/AssignmentCreate.vue";

const assignments = ref([
  { name: 'Finish project', complete: false, id: 1, tag: 'math'},
  { name: 'Read chapter 4', complete: false, id: 2, tag: 'science' },
  { name: 'Turn in homework', complete: false, id: 3, tag: 'math' },
])

const filters = computed(() => {
  return {
    inProgress: assignments.value.filter(assignment => !assignment.complete),
    completed: assignments.value.filter(assignment => assignment.complete)
  }
});

const add = (name) => {
  assignments.value.push({
      name: name,
      complete: false,
      id: assignments.value.length + 1
  });
}

async function fetchData() {
  try {
    // Making a fetch request to the API endpoint
    const response = await fetch('https://tuyord80xi.execute-api.us-east-1.amazonaws.com/dev/todo/all');

    // Checking if the response is successful (status code 200)
    if (!response.ok) {
      throw new Error('Failed to fetch data');
    }

    // Parsing the JSON response
    const data = await response.json();
    console.log(
        data
    )
    assignments.value = data;
  } catch (error) {
    // Handling errors
    console.error('Error fetching data:', error.message);
    return null; // Return null or handle error accordingly
  }
}

onMounted(() => {
  fetchData();
})

</script>

<template>
  <section class="grid h-screen place-content-center space-y-6 bg-gray-800 text-white">
    <AssignmentList title="In Progress" :assignments="filters.inProgress " />
    <AssignmentList title="Completed" :assignments="filters.completed" />

    <AssignmentCreate @add="add"/>
  </section>
</template>

<style>

</style>
