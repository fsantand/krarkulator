<script setup>
import { ref } from 'vue'

defineProps(['label'])
const counter = ref(0)
</script>

<template>
  <div>
    <button class="button u-full-width">{{ label }}</button>
    <input type="number" class="u-full-width" name="generatedMana" />
  </div>
</template>
