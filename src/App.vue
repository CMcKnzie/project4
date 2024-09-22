<script setup>

import AddIngredients from './components/AddIngredients.vue'
import Balance from './components/Balance.vue';
import Header from './components/Header.vue';
import IngredientList from './components/IngredientList.vue'

import {ref, computed, onMounted} from 'vue'

const ingredients = ref([])
const rName = ref('')


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


const handleIngredient = (ingredientData) => {
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
  const savedIngredients = JSON.parse(localStorage.getItem('ingredients'))

  if(savedIngredients){
    ingredients.value=savedIngredients
  }

})



</script>

<template>
  <Header :name="rName"></Header>

  <div class ="container">
      <Balance :total="sum"></Balance>
      <AddIngredients @ingredientSubmitted="handleIngredient"></AddIngredients>
      <IngredientList :ingredients="ingredients" @ingredientDeleted="handleDelete"></IngredientList>

    </div>

</template>