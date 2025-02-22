<script setup>
defineProps(['title'])
const counter = defineModel()
</script>

<template>
  <div>
    <div class="centered">
      <b>{{ title }}</b>
    </div>
    <div class="centered number">
      {{ counter }}
    </div>
  </div>
</template>

<style scoped>
.centered {
  text-align: center;
  vertical-align: middle;
}

.number {
  font-size: 3rem;
}
</style>
