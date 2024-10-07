<template>
    <div class="filters">
      <button @click="setFilter('all')" :class="filter === 'all' ? 'active' : ''">All</button>
      <button @click="setFilter('completed')" :class="filter === 'completed' ? 'active' : ''">Completed</button>
      <button @click="setFilter('pending')" :class="filter === 'pending' ? 'active' : ''">Pending</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        filter: 'all',
      };
    },
    methods: {
      setFilter(filter) {
        this.filter = filter;
        this.$emit('filter-tasks', filter);
      },
    },
  };
  </script>
  
  <style>
  .filters button {
    margin-right: 10px;
  }
  .filters .active {
    font-weight: bold;
  }
  </style>
  