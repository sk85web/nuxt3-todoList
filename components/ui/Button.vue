<script setup>
defineProps({
  children: {
    type: String,
    requored: true,
  },
  callBack: {
    type: Function,
    required: true,
  },
});
</script>

<template>
  <button type="button" @click="callBack">{{ children }}</button>
</template>
