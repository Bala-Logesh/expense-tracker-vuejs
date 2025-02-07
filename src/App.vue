<template>
  <div>
    <Header />
    <div class="container">
      <Balance />
      <IncomeExpenses />
      <TransactionList />
      <AddTransaction />
    </div>
  </div>
</template>

<script>
import Header from './components/Header'
import Balance from './components/Balance'
import IncomeExpenses from './components/IncomeExpenses'
import TransactionList from './components/TransactionList'
import AddTransaction from './components/AddTransaction'

export default {
  components: {
    Header,
    Balance,
    IncomeExpenses,
    TransactionList,
    AddTransaction,
  }
}

</script>

<style></style>
