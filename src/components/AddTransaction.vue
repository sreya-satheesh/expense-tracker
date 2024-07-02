<template>
  <h4>Add new transaction</h4>
  <form id="form" @submit.prevent="onSubmit">

      <input class="form-control my-3" type="text" id="text" placeholder="Enter text" v-model="text" />

      <input
         class="form-control" 
         type="text"
        id="amount"
        placeholder="Enter amount : (negative - expense, positive - income)"
        v-model="amount"
      />

    <button id="addbtn" class="btn btn-success w-100 mt-3">Add</button>
  </form>
</template>

<script setup>
import { useToast } from 'vue-toastification';
import { ref } from 'vue';

const text = ref('');
const amount = ref('');

// Get toast interface
const toast = useToast();

const emit = defineEmits(['transactionSubmitted']);

const onSubmit = () => {
  if (!text.value || !amount.value) {
    // Display a toast error message if either field is empty
    toast.error('Both fields must be filled.');
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit('transactionSubmitted', transactionData);

  // Clear form fields
  text.value = '';
  amount.value = '';
};
</script>
