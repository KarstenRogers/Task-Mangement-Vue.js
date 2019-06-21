<template>
  <div class="task-item">
    <input class="checkbox" type="checkbox" v-model="completed" />
    <div>
      <span
        class="title"
        contenteditable="true"
        @keydown.enter="updateTask($event, task)"
        v-on:blur="updateTask($event, task)"
        :class="{ completed }"
      >
        {{ title }}
      </span>
    </div>
    <div class="remove-item" @click="removeTask(index)">
      &times;
    </div>
  </div>
</template>

<script>
export default {
  name: "task-item",
  props: {
    task: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      id: this.task.id,
      title: this.task.title,
      completed: this.task.completed,
      isComlete: this.task.isComplete
    };
  },
  methods: {
    removeTask(index) {
      this.$emit("removedTask", index);
    },
    updateTask: function(e, task) {
      e.preventDefault();
      task.title = e.target.innerText;
      e.target.blur();
    }
  }
};
</script>
