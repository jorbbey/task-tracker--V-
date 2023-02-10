<template>
  <div
    :class="[task.reminder ? 'reminder' : '', 'task']"
    @dblclick="$emit('toggle-reminder', task.id, 'confirm-reminder')"
  >
    <h3>
      {{ task.text }}
      <i class="fas fa-times" @click="$emit('delete-task', task.id)"></i>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
export default {
  name: 'AppEtask.vue',
  props: {
    task: Object,
  },
  emits: ['toggle-reminder', 'delete-task'],

}
</script>

<style scooped>
.fas {
  color: red;
  font-size: 13px;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 16px;
  margin-bottom: 5px;
}
.task p{
     font-size: 12px;
}
</style>
