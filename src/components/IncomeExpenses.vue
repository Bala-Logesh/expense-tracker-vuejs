<template>
    <div class="inc-exp-container">
        <div>
            <h4>Income</h4>
            <p id="money-plus" class="money plus">+${{ incomeTotal }}</p>
        </div>
        <div>
            <h4>Expense</h4>
            <p id="money-minus" class="money minus">${{ expenseTotal }}</p>
        </div>
    </div>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
    incomeTotal: {
        type: Number,
        required: true
    },
    expenseTotal: {
        type: Number,
        required: true
    }
})
</script>