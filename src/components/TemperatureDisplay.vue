<script setup lang="ts">
defineProps<{
  msg: string;
}>();
</script>

<template>
  <div class="temp-wrapper">
    <h1 class="green">{{ msg }} {{ String.fromCharCode(176) }}</h1>
  </div>
</template>

<style scoped>
.temp-wrapper h1 {
  text-align: center;
  font-weight: 500;
  font-size: 4.6rem;
}
</style>
