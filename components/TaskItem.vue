<script setup>
// import Button from '../components/ui/Button.vue';

defineProps({
  task: {
    type: Object,
    required: true,
  },
  completeTask: {
    type: Function,
    required: true,
  },
  removeTask: {
    type: Function,
    required: true,
  },
});
</script>

<template>
  <div class="tasks-list__item">
    <label :class="{ complited: task.isComplited }">
      <input
        class="checkbox-field"
        type="checkbox"
        @change.stop="completeTask(task.id)"
        :checked="task.isComplited"
      />
      <NuxtLink :to="`/details/${task.id}`" class="tasks-list__link">
        {{ task.title }}
      </NuxtLink>
    </label>
    <!-- <Button :callBack="removeTask(task.id)" children="Delete" /> -->
    <button type="button" @click="removeTask(task.id)">Delete</button>
  </div>
</template>

<style scoped>
.tasks-list__item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 5px;
  border: 1px solid rgb(96, 225, 242);
  border-radius: 5px;
  color: #fff;
  font-size: 1.1rem;
  transition: all 0.2s linear;
}

.tasks-list__link {
  cursor: pointer;
}

.tasks-list__item:has(.tasks-list__link:hover) {
  background-color: rgb(20, 89, 98);
}

.checkbox-field {
  cursor: pointer;
  padding: 5px;
  margin-right: 10px;
}

.complited {
  text-decoration: line-through;
}
</style>
