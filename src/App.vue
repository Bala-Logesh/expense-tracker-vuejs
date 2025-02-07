<template>
  <div>
    <Header />
    <div class="container">
      <Balance :total="+total" />
      <IncomeExpenses :incomeTotal="+incomeTotal" :expenseTotal="+expenseTotal" />
      <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
    </div>
  </div>
</template>

<script setup>
import Header from './components/Header'
import Balance from './components/Balance'
import IncomeExpenses from './components/IncomeExpenses'
import TransactionList from './components/TransactionList'
import AddTransaction from './components/AddTransaction'

import { ref, computed, onMounted } from 'vue'
import { useToast } from 'vue-toastification'

const toast = useToast()

const transactions = ref([])

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'))
  if (savedTransactions) {
    transactions.value = savedTransactions
  }

})

const total = computed(() => {
  return transactions.value.reduce((acc, t) => acc + t.amount, 0).toFixed(2)
})

const incomeTotal = computed(() => {
  return transactions.value.filter(t => t.amount > 0).reduce((acc, t) => acc + t.amount, 0).toFixed(2)
})

const expenseTotal = computed(() => {
  return transactions.value.filter(t => t.amount < 0).reduce((acc, t) => acc + t.amount, 0).toFixed(2)
})

const handleTransactionSubmitted = ({ text, amount }) => {
  const id = Math.floor(Math.random() * 100000)
  transactions.value.push({ id, text, amount })
  saveToLocalStorage()

  toast.success('Transaction added successfully')
}

const handleTransactionDeleted = (transactionId) => {
  console.log(transactionId)
  transactions.value = transactions.value.filter(t => t.id !== transactionId)
  saveToLocalStorage()

  toast.success('Transaction deleted successfully')
}

const saveToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}

</script>

<style></style>
