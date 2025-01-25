<script setup>
import { ref } from 'vue';

const tasks = ref([]);
const newTask = ref({ title: '', id: null, isComplited: false });

const addTask = () => {
  if (!newTask.value.title.trim()) return;

  tasks.value = [
    {
      title: newTask.value.title,
      id: Math.random() * 101,
      isComplited: false,
    },
    ...tasks.value,
  ];

  newTask.value.title = '';
};

const removeTask = (id) => {
  tasks.value = tasks.value.filter((task) => task.id !== id);
};

const completeTask = (id) => {
  const task = tasks.value.find((task) => task.id === id);
  if (task) {
    task.isComplited = !task.isComplited;
  }
};
</script>

<template>
  <div class="container">
    <h1 class="title">Todo List</h1>

    <div class="input__block">
      <input type="text" placeholder="Enter task" v-model="newTask.title" />
      <button type="button" @click="addTask">Add task</button>
    </div>

    <p v-if="!tasks.length" class="empty-list">You haven't any task yet</p>

    <ul class="tasks-list" v-else>
      <li class="tasks-list__item" v-for="task in tasks" :key="task.id">
        <label :class="{ complited: task.isComplited }">
          <input
            class="checkbox-field"
            type="checkbox"
            @change="completeTask(task.id)"
            :checked="task.isComplited"
          />
          {{ task.title }}
        </label>
        <button type="button" @click="removeTask(task.id)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<style>
body {
  font-family: 'Montserrat', sans-serif;
  font-size: 14px;
}

button {
  font-family: inherit;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.2s linear;
  font-weight: normal;
}

button:hover {
  background-color: rgb(96, 225, 242);
}

.container {
  max-width: 320px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: auto;
  width: 100%;
  margin: 0 auto;
  padding: 1rem;
  background: #211f2d;
  border-radius: 10px;
}

.title {
  text-align: center;
  color: rgb(96, 225, 242);
}

.input__block {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1rem;
}

.input__block > input {
  flex-grow: 1;
  padding: 5px;
  border-radius: 5px;
  outline: none;
}

.input__block > input:focus {
  outline: 2px rgb(96, 225, 242);
}

.empty-list {
  color: #fff;
  text-align: center;
  font-size: 1.3rem;
}

.tasks-list {
  list-style: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.tasks-list__item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 5px;
  border: 1px solid rgb(96, 225, 242);
  border-radius: 5px;
  color: #fff;
  font-size: 1.1rem;
}

.checkbox-field {
  padding: 5px;
}

.complited {
  text-decoration: line-through;
}
</style>
