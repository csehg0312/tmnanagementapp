<template>
    <div>
      <div v-for="task in tasks" :key="task.id" class="task-item">
        <TaskItem 
          :task="task"
          @delete-task="handleDeleteTask"
          @toggle-complete="handleToggleComplete"
        />
      </div>
    </div>
  </template>
  
  <script>
  import TaskItem from './TaskItem.vue';
  
  export default {
    props: ['tasks'],
    components: {
      TaskItem,
    },
    methods: {
      handleDeleteTask(id) {
        this.$emit('delete-task', id);
      },
      handleToggleComplete(id) {
        this.$emit('toggle-complete', id);
      },
    },
  };
  </script>
  
  <style>
  .task-item {
    padding: 10px;
    border-bottom: 1px solid #ccc;
  }
  </style>
  