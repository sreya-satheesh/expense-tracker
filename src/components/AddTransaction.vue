<template>
  <form id="form" @submit.prevent="onSubmit" class="d-flex">
    <input class="form-control me-2" type="text" id="text" placeholder="Enter expense" v-model="text" />
    
    <input
      class="form-control me-2"
      type="number"
      id="amount"
      placeholder="Enter amount"
      v-model.number="amount"
      @input="validateAmount"
    />
    
    <button id="addbtn" class="btn btn-success">+</button>
  </form>
</template>

<script setup>
import { useToast } from 'vue-toastification';
import { ref } from 'vue';

const text = ref('');
const amount = ref(null)


const toast = useToast();

const emit = defineEmits(['transactionSubmitted']);

const onSubmit = () => {
  if (!text.value || amount.value === null) {
    toast.error('Both fields must be filled.');
    return;
  }

  const parsedAmount = parseFloat(amount.value);

  if (isNaN(parsedAmount) || parsedAmount === 0) {
    toast.error('Amount must be a valid non-zero number.');
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parsedAmount,
  };

  emit('transactionSubmitted', transactionData);

  text.value = '';
  amount.value = null;
};

const validateAmount = () => {
  if (amount.value === 0) {
    amount.value = null;
    toast.error('Amount cannot be 0.');
  }
};
</script>
