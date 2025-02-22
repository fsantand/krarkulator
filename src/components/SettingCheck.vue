<script setup>
defineProps(['label'])
const model = defineModel({ required: true })

function update() {
  model.value = !model.value
}
</script>

<template>
  <div>
    <button @click="update" class="u-full-width button" :class="{ 'button-primary': model }">
      {{ label }}
    </button>
  </div>
</template>
