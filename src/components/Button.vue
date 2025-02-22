<script setup>
import {ref} from 'vue'

defineProps(['label'])
const counter = ref(0)
</script>

<template>
  <button class="button u-full-width">{{label}}</button>
</template>
