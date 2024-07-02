<template>
  <h4>History</h4>
  <ul id="list" class="list">
    <li 
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.text }} :
      <span class="ms-2">{{ formatAmount(transaction.amount) }}</span>
      <button class="ms-2 btn btn-danger" @click="deleteTransaction(transaction.id)">
        x
      </button>
    </li>
  </ul>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(['transactionDeleted']);

const deleteTransaction = (id) => {
  emit('transactionDeleted', id);
};

const formatAmount = (amount) => {
  // Format amount to display correctly with sign and format
  return amount.toLocaleString('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumFractionDigits: 2,
  });
};
</script>
