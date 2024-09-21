<script setup>

import {defineProps} from 'vue'

const props = defineProps ({
    income: {
        type: Number, 
        require: true, 
    },

    expense: {
        type: Number,
        require: true,
    }
})

</script>

<template>
    <div class="inc-exp-container">
        <div>
            <h4>Income</h4>
            <p class = "money plus" id=money-plus>+${{ income }}</p>
        </div>
    <div>
        <div>
            <h4>Expenses</h4>
            <p class = "money minus" id=money-minus>-${{ expense }}</p>
        </div>
    </div>

    </div>

</template>