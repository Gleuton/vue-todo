<template>
  <div id="app">
    <h1>Tarefas</h1>
    <new-task @taskAdded="addTask" />
    <task-grid @taskDeleted="deleteTasks" :tasks="tasks" />
  </div>
</template>

<script>
import TaskGrid from "./components/TaskGrid";
import NewTask from "./components/NewTask";
export default {
  components: { TaskGrid, NewTask },
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
    deleteTasks(i) {
      this.tasks.splice(i, 1);
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