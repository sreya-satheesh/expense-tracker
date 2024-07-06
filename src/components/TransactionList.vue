<template>
  <div>
    <table v-if="transactions.length > 0" id="transactions-table" class="table mt-5">
      <thead>
        <tr>
          <th>Sr.no</th>
          <th>Expense</th>
          <th>Amount</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr 
          v-for="(transaction, index) in transactions"
          :key="transaction.id"
          :class="transaction.amount < 0 ? 'minus' : 'plus'"
        >
          <td>{{ index + 1 }}</td>
          <td>{{ transaction.text }}</td>
          <td>{{ formatAmount(transaction.amount) }}</td>
          <td>
            <button id="delbtn" class="btn btn-danger" @click="deleteTransaction(transaction.id)">
              x
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

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
  if (amount > 0) {
    return `+ $${amount.toLocaleString('en-US', {
      minimumFractionDigits: 2,
    })}`;
  } else if (amount < 0) {
    return `- $${Math.abs(amount).toLocaleString('en-US', {
      minimumFractionDigits: 2,
    })}`;
  }
};
</script>
