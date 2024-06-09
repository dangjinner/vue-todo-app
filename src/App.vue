<script setup>
import TodoItem from '@/components/TodoItem.vue'
import { ref } from 'vue'

const tasks = ref([
  { id: 1, name: 'Check email', status: 'pending' },
  { id: 2, name: 'Read book', status: 'pending' },
  { id: 3, name: 'Study English', status: 'pending' },
  { id: 4, name: 'Work', status: 'pending' },
  { id: 5, name: 'Have lunch', status: 'pending' },
])

const newTask = ref('')

const editTask = ref(null)

function handleSubmit() {
  if (editTask.value) {
    handleUpdate()
    return
  }

  tasks.value = [
    ...tasks.value,
    {
      id: Math.floor(Math.random() * 1000),
      name: newTask.value,
      status: 'pending'
    }
  ]

  newTask.value = ''
}

function handleUpdateStatus(id) {
  const taskIndex = tasks.value.findIndex((item) => item.id === id)
  console.log(taskIndex)
  tasks.value[taskIndex].status = tasks.value[taskIndex].status === 'done' ? 'pending' : 'done'
}

function handleDelete(id) {
  tasks.value = tasks.value.filter((item) => item.id !== id)
}

function handleEdit(id) {
  const task = tasks.value.find((item) => item.id === id)
  console.log(task)
  editTask.value = task
  newTask.value = task?.name
}

function handleUpdate() {
  const taskIndex = tasks.value.findIndex((item) => item.id === editTask.value.id)
  tasks.value[taskIndex].name = newTask.value
  editTask.value = null
  newTask.value = ''
}
</script>

<template>
  <div class="max-w-md mx-auto bg-white shadow-lg rounded-lg overflow-hidden mt-16">
    <div class="px-4 py-2">
      <h1 class="text-gray-800 font-bold text-2xl uppercase">To-Do List</h1>
    </div>
    <form class="w-full max-w-sm mx-auto px-4 py-2">
      <div class="flex items-center border-b-2 border-teal-500 py-2">
        <input
          class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
          type="text"
          placeholder="Add a task"
          v-model="newTask"
        />
        <button
          class="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
          type="button"
          @click="handleSubmit"
        >
          {{ editTask ? 'Edit' : 'Add' }}
        </button>
      </div>
    </form>
    <ul class="divide-y divide-gray-200 px-4">
      <li v-for="task in tasks" :key="task.id" class="py-4">
        <TodoItem
          :task="task"
          :onDone="handleUpdateStatus"
          :onDelete="handleDelete"
          :onEdit="handleEdit"
        />
      </li>
    </ul>
  </div>
</template>
