<script setup>
import {defineProps} from 'vue';

const props = defineProps({
  balance: {
    type: Number,
    required: true,
  }
})

</script>
<template>
<div class="balance">
  <p class="balance__title">Your Balance</p>
  <p id="balance" class="balance__amount"> ${{props.balance}}</p>
</div>
</template>

<style scoped>
p {
  margin: 0;
}

.balance {
  display: flex;
  flex-direction: column;
  gap: 12px;
  text-align: center;
}

.balance__title {
  font-size: 21px;
  font-weight: bold;
}

.balance__amount {
  font-size: 18px;
}
</style>