<script setup>
import { ref } from 'vue';
import Doing from './components/Doing.vue';
import Done from './components/Done.vue';
import Todo from './components/Todo.vue';

const taskName = ref('');
const tasks = ref([]);

const addTask = () => {
  if (taskName.value.trim() !== '') {
    const taskId = generateTaskId();
    tasks.value.push({
      id: taskId,
      name: taskName.value,
      status: 'TODO'
    });
    taskName.value = '';
    saveTasks();
  }
};

const removeTask = (taskId) => {
  const taskIndex = tasks.value.findIndex(task => task.id === taskId);
  if (taskIndex !== -1) {
    tasks.value.splice(taskIndex, 1);
    saveTasks();
  }
};

const generateTaskId = () => {

  return Date.now().toString();
};

const saveTasks = () => {
  localStorage.setItem('tasks', JSON.stringify(tasks.value));
};

const loadTasks = () => {
  const storedTasks = localStorage.getItem('tasks');
  if (storedTasks) {
    tasks.value = JSON.parse(storedTasks);
  }
};

loadTasks();
</script>

<template>
<header class="head">
  <h1>TASKMANAGER</h1>
  <div className='addtask'>        
    <input
      class="taskinput"
      type="text"
      placeholder="Enter task name"
      v-model="taskName"
    />
    <button @click="addTask">
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" width="30px" stroke="currentColor" class="w-6 h-6">
        <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v6m3-3H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z" />
      </svg>
    </button>
  </div>
</header>
<div class="taskcontainer">
  <Todo :tasks="tasks" :removeTask="removeTask"/>
  <Doing :tasks="tasks" :removeTask="removeTask" />
  <Done :tasks="tasks" :removeTask="removeTask" />
</div>
</template>

<style scoped>
.head {
  width: 100vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  align-items: center;
}
.addtask {
  display: flex;
  flex-direction: row;
  align-items: center;
}
.taskinput {
  padding: 10px;
}
.taskcontainer {
  display: flex;
  flex-direction: row;
  margin-top: 20px;
  justify-content: space-evenly;
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
