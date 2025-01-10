<script setup>
import {defineProps} from 'vue';

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  }
})

const emits = defineEmits(['deleteTransaction'])

const onDeleteTransaction = (id) => {
  emits('deleteTransaction', id)
}

</script>

<template>
  <div class="transaction-list">
<p class="transaction-list__title">History</p>
  <ul v-if="transactions.length" id="list" class="transaction-list__list">
    <li class="transaction-list__item" v-for="transaction in props.transactions" :key="transaction.id">
      <span class="transaction-list__item-title">{{transaction.text}}</span>
      <span id="amount"
            :class="transaction.amount < 0
            ? 'transaction-list__item_minus'
            : 'transaction-list__item_income'"
      >
        ${{transaction.amount}}
      </span>
      <button class="transaction-list__delete" @click="onDeleteTransaction(transaction.id)">X</button>
    </li>
  </ul>
    <p v-else> Your history is empty</p>
  </div>
</template>

<style scoped>
p, ul, li{
  margin: 0;
  padding: 0;
  list-style: none;
}
.transaction-list {
  max-width: 400px;
  padding: 12px;
  border-radius: 8px;
  gap: 16px;
  display: flex;
  flex-direction: column;
  border: 1px solid gray;
  box-shadow: 2px 2px 2px gray;
}
.transaction-list__title{
  font-size: 21px;
  font-weight: bold;
  text-align: center;
  text-transform: uppercase;
}
.transaction-list__list{
  display: flex;
  flex-direction: column;
  width: 100%;
  gap: 8px;
}
.transaction-list__item{
  padding: 4px;
  border-bottom: 1px solid gray;
  border-top: 1px solid gray;
  justify-content: space-between;
  display: flex;
  align-items: center;
  gap: 16px;
}
.transaction-list__item-title {
  width: 200px;
  word-wrap: break-word;
}
.transaction-list__item_minus {
  color: red;
}
.transaction-list__item_income {
  color: green;
}
.transaction-list__delete {
  border-radius: 50%;
  outline: none;
  border: none;
  width: 30px;
  height: 30px;
}
.transaction-list__delete:hover {
  background-color: red;
  color: white;
}
</style>