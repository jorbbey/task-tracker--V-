<template>
  <div v-for="task in tasks" :key="task.id">
    <AppEtask
      :task="task"
      @delete-task="$emit('delete-task', task.id)"
      @toggle-reminder="$emit('toggle-reminder', task.id, 'confirm-reminder')"
    />
  </div>
</template>

<script>
import AppEtask from './AppEtask.vue'
export default {
  name: 'AppTask',
  props: {
    tasks: Array,
  },
  components: {
    AppEtask,
  },
  emits: ['delete-task', 'toggle-reminder'],
}
</script>

<style></style>
