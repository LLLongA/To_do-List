<template>
  <div id="app">
    <task v-bind:tasks="tasks" @clearCompleted="clearCompleted" @clearAll="clearAllTasks" @addTask="addNewTask"></task>
  </div>
</template>

<script>
import Task from "./components/Task";

export default {
  name: "App",
  components: {
    Task,
  },
  data() {
    return {
      tasks: [
        {
          id: 1,
          title: "Prepre Presentation",
          completed: true,
        },
        {
          id: 2,
          title: "Learn Next.js",
          completed: false,
        },
        {
          id: 3,
          title: "Finish Game Assignment",
          completed: false,
        },
        {
          id: 4,
          title: "Send email",
          completed: false,
        },
      ],
    };
  },
  methods: {
    addNewTask(newTaskTitle) {
      const newTask = {
        id: Date.now(),
        title: newTaskTitle,
        completed: false
      };
      this.tasks.push(newTask);
    },

    clearAllTasks() {
      this.tasks = [];
    },
    clearCompleted() {
      this.tasks = this.tasks.filter(task => !this.isCompleted(task));
    },

    isCompleted(task) {
      return task.completed;
    }
  }
};


</script>