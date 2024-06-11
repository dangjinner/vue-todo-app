<script setup>
import { computed } from 'vue'

const props = defineProps({
  task: { type: String, required: true }
})

const emit = defineEmits(['done', 'edit', 'delete'])

const { task } = props

const isDone = computed(() => (task.status === 'done' ? 'line-through' : ''))

function handleDone() {
  emit('done', task.id)
}

function handleEdit() {
  emit('edit', task.id)
}

function handleDelete() {
  emit('delete', task.id)
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
      @click="handleDone"
      :for="task.id"
      class="ml-3 text-gray-900 flex w-full justify-between"
    >
      <div>
        <span class="text-lg font-medium" :class="isDone">{{ task.name }}</span>
        <span class="text-sm font-light text-gray-500"></span>
      </div>
    </label>
    <div class="flex justify-between" style="width: 80px">
      <div class="text-white cursor-pointer" @click="handleEdit">✏️</div>
      <div class="text-white cursor-pointer" @click="handleDelete">❌</div>
    </div>
  </div>
</template>
