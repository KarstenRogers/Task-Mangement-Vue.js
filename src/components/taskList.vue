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
      <div>{{ remaining }} items left</div>
      <button class="clearAll" @click="clearAll()">
        Clear All
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "taskList",
  data() {
    return {
      newTask: "",
      idForTask: [],
      tasks: []
    };
  },
  computed: {
    remaining() {
      return this.tasks.filter(task => !task.completed).length;
    }
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
    },
    clearAll() {
      this.tasks = [];
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
    outline: 1;
    outline-color: black;
  }
}

.task-item {
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: black;
  color: white;
  cursor: pointer;
  transition: all 0.5s ease-in-out;

  &:hover {
    color: black;
    background-color: white;
    transition: all 0.5s ease-in;
  }
}

.remove-item {
  cursor: pointer;
  font-size: 22px;
  color: white;
}

.center {
  text-align: center;
  font-size: 28px;
}

.checkbox {
  height: 20px;
  width: 20px;
  cursor: pointer;
}

.completed {
  text-decoration: line-through;
  color: red;
}

.check-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 20px;
  border-top: 3px solid black;
  padding-top: 10px;
  color: black;
}

.clearAll {
  width: 95px;
  border: 1px solid black;
  font-size: 16px;
  cursor: pointer;
  transition: all 0.5s ease-in-out;

  &:hover {
    background-color: black;
    color: white;
    transition: all 0.5s ease-in-out;
  }
}
</style>
