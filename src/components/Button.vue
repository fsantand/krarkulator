<script setup>
import { ref } from 'vue'
defineProps(['label'])
</script>

<template>
  <button class="button u-full-width">{{ label }}</button>
</template>
