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
          title: "Watch netflix",
          completed: true,
        },
        {
          id: 2,
          title: "Go shopping",
          completed: false,
        },
        {
          id: 3,
          title: "Learn guitar",
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
        id: Date.now(), // 使用时间戳作为唯一 ID
        title: newTaskTitle,
        completed: false
      };
      this.tasks.push(newTask); // 将新任务添加到 tasks 数组
    },
    
    clearAllTasks() {
      this.tasks = []; // 清空 tasks
    },
    clearCompleted() {
      // 过滤掉已经完成的任务
      this.tasks = this.tasks.filter(task => !this.isCompleted(task));
    },
    
    // 判断任务是否完成
    isCompleted(task) {
      return task.completed;
    }
  }
};


</script>