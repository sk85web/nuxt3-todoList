<script setup>
const route = useRoute();
const id = route.params.id;

const task = ref(null);
const isMounted = ref(false);

onMounted(() => {
  const tasks = JSON.parse(localStorage.getItem('tasks'));
  task.value = tasks.find((todo) => todo.id.toString() === id);
  isMounted.value = true;
});
</script>

<template>
  <div class="container">
    <h1 class="title">Task Details</h1>
    <p v-if="isMounted">
      Task title: <span>{{ task.title }}</span>
    </p>

    <NuxtLink class="home-link" to="/">Go Home</NuxtLink>
  </div>
</template>

<style scoped>
p {
  font-size: 1.5rem;
  color: #fff;
}

span {
  font-weight: bold;
}

.home-link {
  text-align: center;
  opacity: 0.7;
  transition: all 0.2s linear;
}

.home-link:hover {
  opacity: 1;
}
</style>
