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

      this.newTask = "";
    }
  },
  data() {
    return {
      newTask: ""
    };
  }
};
</script>
