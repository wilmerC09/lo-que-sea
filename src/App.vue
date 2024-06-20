<script setup>
import { ref } from 'vue'

let newTask = ref('')

let taskList = ref([
  {
    name: 'Estudiar',
    done: true
  },

  {
    name: 'Comer',
    done: false
  },

  {
    name: 'Dormir',
    done: false
  }
])

function addTask() {
  if (newTask.value.trim() === '') return
  taskList.value.push({
    name: newTask.value,
    done: false
  })
  newTask.value = ''
}

function setdone(index) {
  taskList.value[index].done = true
}
</script>

<template>
  <div class="container">
    <h1>Lista de tareas</h1>
    <p class="subtitle">{{ newTask }}</p>
    <div>
      <div class="task" :class="{ done: task.done }" v-for="(task, index) in taskList" :key="index">
        {{ task.name }}
        <span @click="setdone(index)" class="button">X</span>
      </div>
    </div>

    <input
      v-model="newTask"
      @keypress.enter="addTask"
      type="text"
      placeholder="Escriba su tarea"
      maxlength="70"
    />
    <p v-show="newTask != ''" class="help">Presiona Enter para agregar la tarea</p>
  </div>
</template>

<style scoped>
.container {
  color: whitesmoke;
  background-color: #2182bf;
  border-radius: 6px;
  max-width: 420px;
  margin: 0 auto;
  padding: 6px 12px;
  font-family: 'Montserrat', sans-serif;
}

h1 {
  text-transform: uppercase;
  font-size: 18px;
  text-align: center;
  margin: 0;
  margin-top: 12px;
}

.subtitle {
  font-size: 10px;
  margin: 0;
  margin-bottom: 16px;
  text-align: center;
  opacity: 0.6;
}

.task {
  background-color: #52a5d9;
  border-radius: 3px;
  margin-bottom: 1px;
  padding: 2px 2px 1px 6px;
  display: flex;
  justify-content: space-between;
}

.task:hover {
  background-color: #89c2d9;
  transition: background-color 0.3s linear;
}

.button {
  background-color: #0d4373;
  border-radius: 3px;
  display: inline-block;
  padding: 0 6px;
}

.button:hover {
  cursor: pointer;
}

input::placeholder {
  opacity: 0.4;
}

input {
  border: none;
  outline: none;
  border-radius: 3px;
  padding: 2px 6px;
  width: 100%;
  box-sizing: border-box;
  margin-top: 10px;
}

.help {
  font-size: 8px;
  margin: 0;
  opacity: 0.6;
  margin-top: 6px;
  margin-bottom: 4px;
}

.done {
  text-decoration: line-through;
}
</style>
