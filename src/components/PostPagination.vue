<template>
 <div class="btn-group" role="group" aria-label="Basic example">
  <button type="button" class="btn btn-outline-primary" :disabled="inicio <= 0"
   @click="emit('prev')">Prev{{inicio}}</button>
  <button type="button" class="btn btn-outline-primary" :disabled="final >= maxlength" @click="emit('next')">Next{{final}}</button>
 
</div> 
</template>

<script lang='ts' setup>
defineProps([ "inicio", "final", "maxlength"])
const emit = defineEmits([ "next", "prev"])
</script>

<style scoped>
  
</style>