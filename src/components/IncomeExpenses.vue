<template>

  <div class="row my-3">
  <div class="col-sm-6">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">Income</h5>
        <p class="card-text text-success">+${{ income }}</p>
      </div>
    </div>
  </div>
  <div class="col-sm-6">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">Expense</h5>
        <p class="card-text text-danger">{{ formatAmount(expenses) }}</p>
      </div>
    </div>
  </div>
</div>

</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  income: {
    type: Number,
    required: true,
  },
  expenses: {
    type: Number,
    required: true,
  },
});

const formatAmount = (amount) => {
  if (amount < 0) {
    return `- $${Math.abs(amount).toLocaleString('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumFractionDigits: 2,
    }).slice(1)}`; 
  } else {
    return `$${amount.toLocaleString('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumFractionDigits: 2,
    })}`;
  }
};


</script>
