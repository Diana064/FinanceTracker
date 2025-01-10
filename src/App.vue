<script setup>
import Header from "./components/Header.vue";
import Balance from "@/components/Balance.vue";
import IncomeExpense from "@/components/IncomeExpense.vue";
import TransactionList from "@/components/TransactionList.vue";
import AddTransaction from "@/components/AddTransaction.vue";
import {ref, computed, onMounted} from 'vue';

  const transactions = ref([
  {id: 1, text: 'Flower', amount: -20},
  {id: 2, text: 'Salary', amount: 300},
  {id: 3, text: 'Book', amount: -10},
  {id: 4, text: 'Camera', amount: 150}
  ]);


const total = computed( () => {
  return transactions.value.reduce( (acc, transaction) => acc + transaction.amount, 0);
})

const income = computed( () => {
  return transactions.value.filter(transaction => transaction.amount > 0).reduce( (acc, transaction) => acc  + transaction.amount, 0);
})

const expense = computed( () => {
  return transactions.value.filter(transaction => transaction.amount < 0).reduce( (acc, transaction) => acc  + transaction.amount, 0);
})

const handleTransactionSubmitted=(transaction)=> {
  const transactionNewData = {
    id: new Date(),
    text: transaction.text,
    amount: transaction.amount,
  }
  transactions.value.push(transactionNewData);

  savedToLocalStorage()
}

const savedToLocalStorage = () => {
  localStorage.setItem( "transactions", JSON.stringify(transactions.value) );
}

const onDeleteTransaction=(id)=> {
  transactions.value = transactions.value.filter(transaction => transaction.id !== id)

  savedToLocalStorage()
}

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));

  if(savedTransactions){
    transactions.value = savedTransactions;
  }
})


</script>

<template>
  <div class="finance-tracker">
    <Header/>
    <Balance :balance="total" />
    <IncomeExpense :expense="expense" :income="income" />
    <TransactionList :transactions="transactions" @deleteTransaction="onDeleteTransaction"/>
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
  </div>
</template>

<style scoped>
.finance-tracker {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
gap: 16px;
}
</style>
