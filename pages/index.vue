<script setup>
import Button from '../components/ui/Button.vue';

const tasks = ref([]);
const newTask = ref({ title: '', id: null, isComplited: false });

if (typeof window !== 'undefined') {
  tasks.value = JSON.parse(localStorage.getItem('tasks') || []);
}

watch(
  tasks,
  (newTasks) => {
    if (typeof window !== 'undefined') {
      localStorage.setItem('tasks', JSON.stringify(newTasks));
    }
  },
  { deep: true }
);

const addTask = () => {
  if (!newTask.value.title.trim()) return;

  tasks.value.unshift({
    ...newTask.value,
    id: Date.now(),
  });

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
      <Button :callBack="() => addTask()" children="Add" />
    </div>

    <p v-if="!tasks.length" class="empty-list">You haven't any task yet</p>

    <ul class="tasks-list" v-else>
      <li v-for="task in tasks" :key="task.id">
        <TaskItem
          :task="task"
          :completeTask="completeTask"
          :removeTask="removeTask"
        />
      </li>
    </ul>
  </div>
</template>

<style scoped>
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
</style>
