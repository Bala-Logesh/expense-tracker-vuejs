<template>
    <div>
        <h3>History</h3>
        <ul id="list" class="list">
            <li v-for="transaction in transactions" :key="transaction.id"
                :class="transaction.amount > 0 ? 'plus' : 'minus'">
                {{ transaction.text }} <span>${{ transaction.amount }}</span>
                <button class="delete-btn" @click="deleteTransaction(transaction.id)">x</button>
            </li>
        </ul>
    </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

const emit = defineEmits(['transactionDeleted'])

const props = defineProps({
    transactions: {
        type: Array,
        required: true
    }
})

const deleteTransaction = (transactionId) => {
    console.log(transactionId)
    emit('transactionDeleted', transactionId)
}
</script>