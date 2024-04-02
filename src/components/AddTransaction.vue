<template>
    <h3>Add new transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
      <div class="form-control">
        <label for="text">Text</label>
        <input type="text" id="text" v-model="text" placeholder="Enter text..." />
      </div>
      <div class="form-control">
        <label for="amount">Amount <br />
          (negative - expense, positive - income)</label>
        <input type="number" id="amount" v-model="amount" placeholder="Enter amount..." step="any" />
      </div>
      <button class="btn">Add transaction</button>
    </form>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import { useToast } from 'vue-toastification';
  
  const text = ref('');
  const amount = ref(0);
  const emit = defineEmits(['transactionSubmitted']);
  const toast = useToast();
  
  const onSubmit = () => {
    if (!text.value.trim()) {
      toast.error('Text field is required');
      return;
    }
    if (amount.value === 0) {
      toast.error('Amount field is required');
      return;
    }
  
    // Define the transaction data inside the onSubmit function
    const transactionData = {
      text: text.value,
      amount: parseFloat(amount.value),
    };
  
    // Emit the event inside the onSubmit function after validations pass
    emit('transactionSubmitted', transactionData);
  
    // Reset form fields after submission
    text.value = '';
    amount.value = 0;
  };
  </script>
  