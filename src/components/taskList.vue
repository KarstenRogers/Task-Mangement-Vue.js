<template>
  <div>
    <p class="center">Task Management</p>
    <input
      type="text"
      class="task-input"
      placeholder="New Task"
      v-model="newTask"
      @keyup.enter="addTask"
    />
    <div v-for="(task, index) in tasks" :key="task.id" class="task-item">
      <div>
        {{ task.title }}
      </div>
      <div class="remove-item" @click="removeTask(index)">
        &times;
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "taskList",
  data() {
    return {
      newTask: "",
      idForTask: 1,
      tasks: []
    };
  },
  methods: {
    addTask() {
      this.tasks.push({
        id: this.idForTask,
        title: this.newTask,
        completed: false
      });

      this.newTask = "";
      this.idForTask++;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<style lang="scss">
.task-input {
  width: 100%;
  padding: 6px 13px;
  font-size: 18px;
  margin-bottom: 15px;

  &:focus {
    outline: 0;
  }
}

.task-item {
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: lightgray;
  color: black;
}

.remove-item {
  cursor: pointer;
  font-size: 20px;
    color: black;
}

.center {
  text-align: center;
  font-size: 28px;
}
</style>
