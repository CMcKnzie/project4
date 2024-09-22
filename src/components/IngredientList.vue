<script setup>

import {defineProps, defineEmits} from 'vue'

const props = defineProps ({
    ingredients: {
    type: Array, 
    require: true,
    }
})


const emit = defineEmits (['ingredientDeleted'])

const deleteIngredient = (id) => {
    emit('ingredientDeleted', id)
}

</script>

<template>
 
 <h3>Recipe List</h3>
 <ul class ="list" id="list">
    <li v-for="x in ingredients" v-bind:key="x.id"
    v-bind:class="x.amount < 0 ? 'minus' : 'plus'">
    {{ x.text }} <span> ${{ x.amount }}</span>
    <button @click="deleteIngredient(x.id)" class="delete-btn">X</button>

    </li>
 </ul>

</template>