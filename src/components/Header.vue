<script setup>

import {onMounted, ref, watch} from 'vue'

const rName = ref('')

onMounted(() => {
  rName.value = localStorage.getItem('rName') || ''
})

watch(rName, (newVal) => {
  localStorage.setItem('rName', newVal)
}, {deep: true})


</script>

<template>
  <h2>Recipe Saver: {{rName}}</h2>
  
  <form id="recipe">
        <div class= "form-control">
            <label for="rName">Enter Recipe Name</label>
            <input type="text" id="text" v-model="rName" placeholder="Enter recipe name">
        </div>
        </form>
  
</template>