<template>
  <div class="task-input">
    <input
      type="text"
      class="task-input"
      placeholder="New Task"
      v-model="newTask"
      @keyup.enter="addTask"
    />
  </div>
</template>

<script>
export default {
  name: "task-input",
  methods: {
    addTask(index) {
      this.$emit("addTask", index);
      this.tasks.push({
        id: this.idForTask,
        title: this.newTask,
        completed: false
      });
      this.newTask = "";
      this.idForTask++;
    }
  },
  data() {
    return {
      tasks: [],
        idForTask: 1,
    };
  }
};
</script>
