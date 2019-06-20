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
    <div
      v-for="(task, index) in tasks"
      :key="task.id"
      class="task-item"
      :class="{ completed: task.completed }"
    >
      <input class="checkbox" type="checkbox" v-model="task.completed" />
      <div>
        {{ task.title }}
      </div>
      <div class="remove-item" @click="removeTask(index)">
        &times;
      </div>
    </div>

    <div class="check-container">
      <div>
        <label><input type="checkbox" :checked="!taskRemaining" /> Check All</label>
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
  },
  mounted() {
    if (localStorage.getItem("tasks"))
      this.tasks = JSON.parse(localStorage.getItem("tasks"));
  },
  watch: {
    tasks: {
      handler() {
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
      },
      deep: true
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
  background-color: #f2f2f2;
  color: black;
}

.remove-item {
  cursor: pointer;
  font-size: 22px;
  color: black;
}

.center {
  text-align: center;
  font-size: 28px;
}

.checkbox {
  height: 20px;
  width: 20px;
}

.completed {
  text-decoration: line-through;
  color: red;
}

    .check-container {
        display: flex;
        align-items: center;
        justify-content: space-between;
        font-size: 16px;
        border-top: 1px solid lightgray;
        padding-top: 14px;
        margin-bottom: 14px;
    }
</style>
