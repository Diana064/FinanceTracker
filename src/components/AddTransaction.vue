<script setup>
import {ref} from 'vue'
import {useToast} from "vue-toastification";

const amount = ref('')
const text = ref('')

const emit = defineEmits(['transactionSubmitted'])

const toast = useToast()

const onSubmit = () => {
  if(!text.value || !amount.value) {
    toast.error('Both fields must be filled!')
    return
  }
toast.success('Transaction added successfully!')
  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  }

  emit('transactionSubmitted', transactionData)

  resetFormData()
}

const resetFormData= () => {
  text.value = ''
  amount.value = ''
}


</script>

<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input v-model="text" type="text" id="text" placeholder="Enter text..." />
    </div>
    <div class="form-control">
      <label for="amount"
      >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input v-model="amount" type="number" id="amount" placeholder="Enter amount..." />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<style scoped>
/* Стилі для форми */
#form {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 400px;
  box-sizing: border-box;
}

/* Заголовок */
h3 {
  text-align: center;
  color: #333;
}

/* Стилі для полів вводу */
.form-control {
  margin-bottom: 20px;
}

.form-control label {
  font-weight: bold;
  display: block;
  margin-bottom: 5px;
  color: #333;
}

.form-control input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-sizing: border-box;
}

.form-control input:focus {
  outline: none;
  border-color: #4caf50;
  box-shadow: 0 0 5px rgba(76, 175, 80, 0.3);
}

/* Стилі для кнопки */
button.btn {
  width: 100%;
  padding: 12px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button.btn:hover {
  background-color: #45a049;
}
</style>