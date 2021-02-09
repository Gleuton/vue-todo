<template>
  <div id="task-grid">
    <template v-if="tasks.length">
      <Task v-for="task in tasks" :key="task.name" :task="task"> </Task>
    </template>
    <p v-else class="no-task">Lista vazia! Nada para fazer.</p>
  </div>
</template>

<script>
import Task from "./Task";

export default {
  name: "TaskGrid",
  components: { Task },
  props: {
    tasks: { type: Array, required: true },
  },
};
</script>

<style>
#task-grid {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
#task-grid .task {
  margin: 11px;
}
.no-task {
  color: #AAA;
  font: 2em sans-serif;
}
</style>