<script setup>

import {ref} from "vue";


const tasks = ref([
  {
    name: "Task 1",
    time: 30
  },
  {
    name: "Task 2",
    time: 40
  },
  {
    name: "Task 3",
    time: 60
  },
  {
    name: "Task 4",
    time: 45
  },
  {
    name: "Task 5",
    time: 50
  },
]);

const showEditModal = ref(null);
const taskToEdit = ref({});

function showEditForm(index) {
  taskToEdit.value = tasks.value[index];
  showEditModal.value = index;
}

function updateTask(index) {
  tasks.value[index] = taskToEdit.value;
  showEditModal.value = null;
}

</script>

<template>

  <div class="container mx-auto p-4">
    <h1 class="text-2xl font-bold mb-4">Tasks</h1>
    <ul class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
      <li v-for="(task, index) in tasks" :key="index" class="bg-white shadow rounded-lg p-4">
        <h2 class="text-lg font-medium bg-red-400 text-white py-2 px-4 rounded-lg mb-2">
          Task Name: {{ task.name }}
        </h2>
        <p class="text-gray-700 mt-2">Time: {{ task.time }}</p>

        <div class="flex items-center justify-between mt-4">
          <button @click="showEditForm(index)" class="text-blue-500 bg-black-400 hover:underline py-2 px-4 rounded-full">
            Edit
          </button>
        </div>

        <!-- Edit Modal -->
        <teleport to="body">
          <div v-if="showEditModal === index" class="fixed z-50 inset-0 overflow-y-auto">
            <div class="flex items-center justify-center min-h-screen p-4 sm:p-0">
              <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" aria-hidden="true"></div>
              <div class="inline-block bg-white rounded-lg overflow-hidden shadow-xl transform transition-all max-w-lg w-full">
                <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
                  <div class="sm:flex sm:items-start">
                    <div class="text-center sm:mt-0 sm:ml-4 sm:text-left">
                      <h3 class="text-lg leading-6 font-medium text-gray-900">
                        Edit Task
                      </h3>
                      <div class="mt-2">
                        <form @submit.prevent="updateTask(index)">
                          <div class="mb-4">
                            <label for="task-name" class="block text-gray-700 font-bold mb-2">Name:</label>
                            <input type="text" id="task-name" v-model="taskToEdit.name" class="input-field">
                          </div>
                          <div class="mb-4">
                            <label for="task-time" class="block text-gray-700 font-bold mb-2">Time:</label>
                            <input type="number" id="task-time" v-model.number="taskToEdit.time" class="input-field">
                          </div>
                          <button type="submit" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full">
                            Update Task
                          </button>
                        </form>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="bg-gray-50 px-4 py-3 sm:px-6 sm:flex sm:flex-row-reverse">
                  <button @click="showEditModal = null" type="button" class="w-full inline-flex justify-center rounded-md border border-transparent shadow-sm px-4 py-2 bg-red-600 text-base font-medium text-black hover:bg-blue-50 focus:outline-none">
                    Cancel
                  </button>
                  <button class="w-full inline-flex justify-center">

                  </button>
                </div>
              </div>
            </div>
          </div>
        </teleport>
      </li>
    </ul>
  </div>

  <button class="inline-flex text-3xl text-white items-center hover:text-red-950">
    Testing Button
  </button>


</template>

<style scoped>

</style>
