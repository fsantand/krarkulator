<script setup>
import { ref } from 'vue'

defineProps(['label'])
const active = false;
</script>

<template>
  <div>
    <button
      @click="active = !active"
      class="u-full-width"
      :class="{active: button-primary}">{{label}}</button>
  </div>
</template>
