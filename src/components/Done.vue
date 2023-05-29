<template>
    <div class="done">
        <div class="head">
      <h2>DONE</h2>
        </div>
      <div v-for="task in filteredTasks" :key="task.id" class="task">
        <h4>{{ task.name }}</h4>
        <div class="controls">
          <button @click="removeTask(task.id)">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" height="30px"  stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M9.75 9.75l4.5 4.5m0-4.5l-4.5 4.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['tasks', 'removeTask'],
    methods: {
      markTaskAsDone(taskId) {
        const taskIndex = this.tasks.findIndex(task => task.id === taskId);
        if (taskIndex !== -1) {
          this.tasks[taskIndex].status = 'DONE';
          this.saveTasks();
        }
      },
      saveTasks() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
      },
    },
    computed: {
      filteredTasks() {
        return this.tasks.filter(task => task.status === 'DONE');
      }
    }
  };
  </script>
  
  <style scoped>
  .done {
    width: 30%;
  }

  .head {
    color: #FFFFFF;
    background-color: #3B3B3B;
    border-radius: 10px;
    padding: 10px;
  }
  .task {
    margin-top: 10px;
    padding: 10px;
    background-color: #F4F4F4;
    border-radius: 10px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }
  .controls {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
  }
  button {
	background: none;
	color: inherit;
	border: none;
	padding: 0;
	font: inherit;
	cursor: pointer;
	outline: inherit;
    margin-right: 10px;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
}
  </style>
  