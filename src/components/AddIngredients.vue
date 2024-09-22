<script setup>

import {ref} from 'vue'

const text = ref('')
const amount = ref('')

const emit = defineEmits([
    'ingredientSubmitted'
])

const onSubmit =() =>{
    const ingredientData = {
        text: text.value, 
        amount: parseFloat(amount.value),
    }
    emit('ingredientSubmitted', ingredientData)

    text.value =''
    amount.value=''
}

</script>

<template>
    <h3>Add a new ingredient</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class= "form-control">
            <label for="text">Enter Ingredient</label>
            <input type="text" id="text" v-model="text" placeholder="Enter Ingredient Name e.g. milk">
        </div>

        <div class= "form-control">
            <label for="text">Enter Ingredient Cost</label>
            <input type="text" id="amount" v-model="amount" placeholder="Ingredient Cost">
        </div>

        <button class="btn">Add Ingredient</button>

    </form>

</template>