<script setup>
import { computed } from 'vue'

const props = defineProps({
  task: String,
  onDone: Function,
  onDelete: Function,
  onEdit: Function,
})

const { task, onDone, onEdit } = props

const isDone = computed(() => (task.status === 'done' ? 'line-through' : ''))

function handleDoneTask() {
  onDone(task.id)
}
</script>

<template>
  <div class="flex items-center">
    <input
      :id="task.id"
      :name="task.id"
      type="checkbox"
      class="h-4 w-4 text-teal-600 focus:ring-teal-500 border-gray-300 rounded"
    />
    <label
      @click="handleDoneTask"
      :for="task.id"
      class="ml-3 text-gray-900 flex w-full justify-between"
    >
      <div>
        <span class="text-lg font-medium" :class="isDone">{{ task.name }}</span>
        <span class="text-sm font-light text-gray-500"></span>
      </div>
    </label>
    <div class="flex justify-between" style="width: 80px;">
      <div class="text-white cursor-pointer" @click="onEdit(task.id)">✏️</div>
      <div class="text-white cursor-pointer" @click="onDelete(task.id)">❌</div>
    </div>
  </div>
</template>
