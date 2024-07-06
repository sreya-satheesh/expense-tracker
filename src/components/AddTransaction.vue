<template>
  <form id="form" @submit.prevent="onSubmit" class="d-flex">
    <input class="form-control me-2" type="text" id="text" placeholder="Enter expense" v-model="text" />
    
    <input
      class="form-control me-2"
      type="number"
      id="amount"
      placeholder="Enter amount"
      v-model.number="amount"
    />
    
    <button id="addbtn" class="btn btn-success">+</button>
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
