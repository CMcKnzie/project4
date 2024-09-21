<script setup>
import {defineProps} from 'vue'

const props = defineProps ({
  total: {
    type: Number, 
    require: true,
  }

}) 
</script>

<template>
  <h4>Recipe Cost</h4>
  <h1 id="balance">$ {{total}}</h1>
</template>