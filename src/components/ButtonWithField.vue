<script setup>
defineProps(['label', 'callback'])
defineEmits([ 'onCast' ]);
const model = defineModel()
</script>

<template>
  <div>
    <button @click="$emit('onCast')" class="button u-full-width">{{ label }}</button>
    <input type="number" class="u-full-width" name="generatedMana" v-model.number="model"/>
  </div>
</template>
