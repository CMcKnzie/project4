<script setup>

import AddIngredients from './components/AddIngredients.vue'
import Balance from './components/Balance.vue';
import Header from './components/Header.vue';
import CostTracker from './components/CostTracker.vue';
import IngredientList from './components/IngredientList.vue'

import {ref, computed, onMounted} from 'vue'

const ingredients = ref([])

const sum = computed(() => {
  return ingredients.value.reduce((acc, x) => {
      return acc+x.amount
  },0)
})

const inIn = computed(() => {
  return ingredients.value
  .filter((x)=>x.amount>0)
  .reduce((acc, x) => {
      return acc+x.amount
  },0)
})

const inOut = computed(() => {
  return ingredients.value
  .filter((x)=>x.amount<0)
  .reduce((acc, x) => {
      return acc+x.amount
  },0)
})

const handleingredient = (ingredientData) => {
  ingredients.value.push ({
  text: ingredientData.text,
  amount: ingredientData.amount, 
  id:generateID(),
  
  })
  saveToLocalStorage()
}

const generateID =() => {
  return Math.floor(Math.random() * 10000000)
}

const handleDelete =(id) => {
  ingredients.value = ingredients.value.filter((x)=> x.id !== id)
  saveToLocalStorage()

}

const saveToLocalStorage=() =>{
  localStorage.setItem('ingredients', JSON.stringify(ingredients.value))
}

onMounted(() => {
  const savedingredients = JSON.parse(localStorage.getItem('ingredients'))
  if(savedingredients){
    ingredients.value=savedingredients
  }
})

</script>

<template>
  <Header></Header>

  <div class ="container">
      <Balance :total="sum"></Balance>
      <Addingredients @ingredientSubmitted="handleIngredient"></Addingredients>
      <IncomeExpenses :income="inIn" :expense="inOut"></IncomeExpenses>
      <ingredientHistory :ingredients="ingredients" @ingredientDeleted="handleDelete"></ingredientHistory>

    </div>

</template>