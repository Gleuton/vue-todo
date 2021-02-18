<template>
  <div class="new-task">
    <input
      v-model="name"
      @keydown.enter="add"
      type="text"
      class="form-element"
      name="task"
      id="task"
      placeholder="Nova Tarefa"
    />
    <button class="form-element" @click="add">+</button>
  </div>
</template>

<script>
export default {
  name: "NewTask",
  data() {
    return {
      name: "",
    };
  },
  methods: {
    add() {
      this.$emit("taskAdded", { name: this.name });
      this.name = "";
    },
  },
};
</script>

<style>
.new-task {
  margin: 30px;
}

.form-element {
  outline: none;
  font-size: 2rem;
  border: 1px solid #fff;
  padding: 5px 10px;
  color: #fff;
}

input.form-element {
  border-right: none;
  width: 500px;
  background-color: #fff2;
  border-radius: 8px 0 0 8px;
}

button.form-element {
  cursor: pointer;
  border-left: none;
  background: #2d5692;
  border-radius: 0 8px 8px 0;
}
</style>