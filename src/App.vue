<template>
  <div>
    <Header />
    <div class="container">
      <Balance :total="total" />
      <IncomeExpenses :incomeTotal="incomeTotal" :expenseTotal="expenseTotal" />
      <TransactionList :transactions="transactions" />
      <AddTransaction />
    </div>
  </div>
</template>

<script setup>
import Header from './components/Header'
import Balance from './components/Balance'
import IncomeExpenses from './components/IncomeExpenses'
import TransactionList from './components/TransactionList'
import AddTransaction from './components/AddTransaction'

import { ref, computed } from 'vue'

const transactions = ref([
  { id: 1, text: 'Flower', amount: -19.99 },
  { id: 2, text: 'Salary', amount: 299.97 },
  { id: 3, text: 'Book', amount: -10 },
  { id: 4, text: 'Camera', amount: 150 }
])

const total = computed(() => {
  return transactions.value.reduce((acc, t) => acc + t.amount, 0)
})

const incomeTotal = computed(() => {
  return transactions.value.filter(t => t.amount > 0).reduce((acc, t) => acc + t.amount, 0).toFixed(2)
})

const expenseTotal = computed(() => {
  return transactions.value.filter(t => t.amount < 0).reduce((acc, t) => acc + t.amount, 0).toFixed(2)
})

</script>

<style></style>
