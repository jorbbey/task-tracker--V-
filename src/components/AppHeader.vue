<template>
  <header>
    <h1>{{ title }}</h1>
    <AppButton
      :text="showAddTask ? 'Close' : 'Add Task'"
      :color="showAddTask ? 'red' : 'green'"
      @btn-click="$emit('toggle-add-task')"
    />
  </header>
</template>

<script>
import AppButton from './AppButton.vue'
export default {
  name: 'AppHeader',
  props: {
    title: String,
    showAddTask: Boolean
  },
  components: {
    AppButton,
  },
}
</script>

<style scooped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
