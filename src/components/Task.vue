<template>
  <div class="container">
    <div class="task">
      <!-- title -->
      <div class="title">
        <h1>To Do List</h1>
      </div>
      <!-- form -->
      <div class="form">
        <input type="text" placeholder="New Task" v-model="newTask" @keyup.enter="addTask" />
        <button><i @click="addTask" class="fas fa-plus"></i></button>
      </div>
      <!-- task lists -->
      <div class="taskItems">
        <ul>
          <task-item v-bind:task="task" v-for="(task, index) in tasks" :key="task.id" @remove="removeTask(index)"
            @complete="completeTask(task)"></task-item>
        </ul>
      </div>
      <!-- buttons -->
      <div class="clearBtns">
        <button @click="$emit('clearCompleted')">Clear completed</button>
        <button @click="$emit('clearAll')">Clear all</button>
      </div>
      <!-- pending task -->
      <div class="pendingTasks">
        <span>Pending Tasks: {{ pendingTasks }} </span>
      </div>
    </div>
  </div>
</template>

<script>

import TaskItem from './Task-item.vue';

export default {
  name: "Task",
  props: ['tasks'],
  components: { TaskItem },
  data() {
    return {
      newTask: ''
    };
  },
  computed: {
    pendingTasks() {
      return this.tasks.filter(task => !task.completed).length;
    }
  },

  methods: {
    addTask() {
      if (this.newTask.trim()) {
        // 触发 addTask 事件，并将新任务的标题传递给父组件
        this.$emit('addTask', this.newTask.trim());
        this.newTask = ''; // 清空输入框
      }
    },

    removeTask(index) {
      this.tasks.splice(index, 1);
    },

    completeTask(task) {
      task.completed = !task.completed;
    }
  }
};
</script>
