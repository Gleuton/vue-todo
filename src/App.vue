<template>
  <div id="app">
    <h1>Tarefas</h1>
    <TasksProgress :progress="progress" />
    <new-task @taskAdded="addTask" />
    <task-grid
      :tasks="tasks"
      @taskDeleted="deleteTasks"
      @taskStateChanged="toggleTaskState"
    />
  </div>
</template>

<script>
import TasksProgress from "./components/TasksProgress";
import TaskGrid from "./components/TaskGrid";
import NewTask from "./components/NewTask";

export default {
  components: { TaskGrid, NewTask, TasksProgress },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    addTask(task) {
      const isSameName = (t) => t.name === task.name;
      const isNew = this.tasks.filter(isSameName).length == 0;
      if (isNew && task.name) {
        this.tasks.push({
          name: task.name,
          pending: task.pending || true,
        });
      }
    },
    toggleTaskState(i) {
      this.tasks[i].pending = !this.tasks[i].pending;
    },
    deleteTasks(i) {
      this.tasks.splice(i, 1);
    },
  },
  computed: {
    progress() {
      const total_tasks = this.tasks.length;
      const done_tasks = this.tasks.filter((task) => !task.pending).length;
      const result = (done_tasks / total_tasks) * 100 || 0;
      return result.toFixed(1);
    },
  },
};
</script>

<style>
body {
  font-family: "Lato", sans-serif;
  background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
  color: #fff;
}

#app {
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app h1 {
  margin-bottom: 5px;
  font-weight: 300;
  font-size: 3rem;
}
</style>