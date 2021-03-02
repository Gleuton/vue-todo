<template>
  <div class="task" :class="stateClass">
    <span @click="$emit('taskDeleted', task)" class="close">x</span>
    <p>{{ task.name }}</p>
  </div>
</template>

<script>
export default {
  props: {
    task: { type: Object, required: true },
  },
  computed: {
    stateClass() {
      return {
        pending: this.task.pending,
        done: !this.task.pending,
      };
    },
  },
};
</script>

<style>
.task {
  position: relative;
  box-sizing: border-box;
  width: 350px;
  height: 150px;
  padding: 10px;
  border-radius: 10px;
  cursor: pointer;
  font-size: 2rem;
  font-weight: 400;
  display: flex;
  justify-content: center;
  align-content: center;
  align-items: center;
  user-select: none;
}

.pending {
  border-left: 15px solid #b73229;
  background-color: #f44336;
}

.done {
  color: #ddd;
  border-left: 15px solid #0a8f08;
  background-color: #4caf50;
  text-decoration: line-through;
}

.close {
  position: absolute;
  right: 10px;
  top: 10px;
  width: 20px;
  height: 20px;
  border-radius: 100%;
  font-size: 0.9rem;
  font-weight: 600;
  text-align: center;
}

.pending .close {
  background-color: #b73229;
}

.done .close {
  background-color: #0a8f08;
}
</style>