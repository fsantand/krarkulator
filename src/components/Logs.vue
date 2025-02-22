<script setup>
const logs = defineModel()
</script>

<template>
  <div v-for="log in logs.slice().reverse()">
    - {{log.message}}
  </div>
</template>
