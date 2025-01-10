<script setup>
import {defineProps} from "vue";

const props = defineProps({
  income: {
    type: Number,
    required: true,
  },
  expense: {
    type: Number,
    required: true,
  }
})
</script>

<template>
<div class="income-expense">
  <div class="income-expense__buttons">
    <p>Income</p>
    <p id="money-plus" class="income-expense__buttons_minus">+${{props.income}}</p>
  </div>
  <div class="income-expense__buttons">
    <p>Expense</p>
    <p id="money-minus" class="income-expense__buttons_plus">${{props.expense}}</p>
  </div>
</div>
</template>

<style scoped>
p {
  margin: 0;
}
.income-expense {
  display: flex;
  text-transform: uppercase;
  gap: 12px;
  font-weight: bold;
}
.income-expense__buttons {
  display: flex;
  flex-direction: column;
  gap: 8px;
  align-items: center;
  padding: 12px;
  border: 1px solid gray;
  border-radius: 8px;
  cursor: pointer;
  box-shadow: 2px 2px 2px gray;
}
.income-expense__buttons:focus, .income-expense__buttons:hover {
  background-color: #f2f2f2;
}

.income-expense__buttons_minus {
  color: green;
}
.income-expense__buttons_plus {
  color: red;
}
</style>