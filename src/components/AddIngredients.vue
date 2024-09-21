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
            <label for="text">Enter ingredient</label>
            <input type="text" id="text" v-model="text" placeholder="Enter ingredient">
        </div>

        <div class= "form-control">
            <label for="text">Enter ingredient Cost</label>
            <input type="text" id="amount" v-model="amount" placeholder="Enter Negative Value for Expenses">
        </div>

        <button class="btn">Add ingredient</button>

    </form>

</template>