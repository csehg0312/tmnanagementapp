<template>
    <div :class="task.completed ? 'completed' : ''" class="task-item">
      <input type="checkbox" v-model="task.completed" @change="toggleComplete" />
      <strong>{{ task.title }}</strong>
      <p>{{ task.description }}</p>
      <small>{{ task.category }}</small>
      <button @click="deleteTask" class="btn-delete">Delete</button>
    </div>
  </template>
  
  <script>
  export default {
    props: ['task'],
    methods: {
      deleteTask() {
        this.$emit('delete-task', this.task.id);
      },
      toggleComplete() {
        this.$emit('toggle-complete', this.task.id);
      },
    },
  };
  </script>
  
  <style>
  .task-item {
    display: flex;
    flex-direction: column;
    margin-bottom: 10px;
  }
  .completed {
    text-decoration: line-through;
    color: gray;
  }
  .btn-delete {
    background-color: red;
    color: white;
    padding: 5px;
    border: none;
    cursor: pointer;
  }
  </style>
  