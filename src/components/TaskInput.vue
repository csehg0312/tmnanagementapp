<template>
    <form @submit.prevent="submitTask" class="mb-4">
      <input v-model="title" type="text" placeholder="Task Title" class="input" required />
      <textarea v-model="description" placeholder="Task Description" class="input"></textarea>
      <select v-model="category" class="input">
        <option value="Work">Work</option>
        <option value="Personal">Personal</option>
        <option value="School">School</option>
      </select>
      <button type="submit" class="btn">Add Task</button>
    </form>
  </template>
  
  <script>
  export default {
    data() {
      return {
        title: '',
        description: '',
        category: 'Work',
      };
    },
    methods: {
      submitTask() {
        const task = {
          id: Date.now(),
          title: this.title,
          description: this.description,
          category: this.category,
          completed: false,
        };
        this.$emit('add-task', task);
        this.title = '';
        this.description = '';
        this.category = 'Work';
      },
    },
  };
  </script>
  
  <style>
  .input {
    display: block;
    width: 100%;
    padding: 8px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
  }
  .btn {
    background-color: #007bff;
    color: white;
    padding: 10px 15px;
    border: none;
    cursor: pointer;
  }
  </style>
  