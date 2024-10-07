<template>
  <div>
    <div class="min-h-screen p-4">
      <button @click="toggleDarkMode" class="mb-4 px-4 py-2 border">
        Toggle {{ isDarkMode ? 'Light' : 'Dark' }} Mode
      </button>
      <TaskInput @add-task="addTask" />
      <TaskFilters @filter-tasks="filterTasks" />
      <TaskList 
        :tasks="filteredTasks" 
        @delete-task="deleteTask" 
        @toggle-complete="toggleComplete"
      />
    </div>
  </div>
</template>

<script>
import TaskInput from '../components/TaskInput.vue';
import TaskList from '../components/TaskList.vue';
import TaskFilters from '../components/TaskFilters.vue';

export default {
  components: {
    TaskInput,
    TaskList,
    TaskFilters,
  },
  data() {
    return {
      tasks: JSON.parse(localStorage.getItem('tasks')) || [],
      filter: 'all',
      isDarkMode: localStorage.getItem('isDarkMode') === 'true',  // Load dark mode state from local storage
    };
  },
  computed: {
    filteredTasks() {
      if (this.filter === 'completed') return this.tasks.filter(task => task.completed);
      if (this.filter === 'pending') return this.tasks.filter(task => !task.completed);
      return this.tasks;
    },
  },
  methods: {
    addTask(task) {
      this.tasks.push(task);
      this.saveTasks();
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
      this.saveTasks();
    },
    toggleComplete(id) {
      const task = this.tasks.find(task => task.id === id);
      task.completed = !task.completed;
      this.saveTasks();
    },
    filterTasks(filter) {
      this.filter = filter;
    },
    toggleDarkMode() {
      this.isDarkMode = !this.isDarkMode;
      localStorage.setItem('isDarkMode', this.isDarkMode ? 'true' : 'false');
      this.applyDarkMode();
    },
    applyDarkMode() {
      if (this.isDarkMode) {
        document.body.style.backgroundColor = '#0f0f0f';
        document.body.style.color = '#f0f0f0';
      } else {
        document.body.style.backgroundColor = '#f0f0f0';
        document.body.style.color = '#0f0f0f0';
      }
    },
    saveTasks() {
      try {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
      } catch (error) {
        console.error('Error saving tasks:', error);
      }
    },
  },
  mounted() {
    this.applyDarkMode(); // Apply dark mode on page load based on local storage value
  }
};
</script>

<style>
/* Ensure tailwind or custom dark mode styles */
dark {
  background-color: #0f0f0f; /* Dark background */
  color: #f0f0f0; /* Light text */
}

html {
  background-color: #0f0f0f; /* Dark background */
  color: #f0f0f0; /* Light text */
}

html {
  background-color: #f0f0f0;
  color: #0f0f0f;
}

button {
  background-color: #4a5568; /* Light gray by default */
  color: white;
}

.dark button {
  background-color: #2d3748; /* Darker button in dark mode */
  color: white;
}
</style>
