<template>

  <div class="row mt-5">
  <div class="col-sm-6">
    <div class="card">
      <div class="card-body">
        <p class="card-title">Total Income : <span class="text-success">{{ formatAmount(income) }}</span></p>
      </div>
    </div>
  </div>
  <div class="col-sm-6">
    <div class="card">
      <div class="card-body">
        <p class="card-title">Total Expense : <span class="text-danger">{{ formatAmount(expenses) }}</span></p>
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

const formatAmount = (amount) => 
{
  if (amount < 0) 
  {
    return `- $${Math.abs(amount).toLocaleString('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumFractionDigits: 2,
    }).slice(1)}`; 
  }
  else if(amount > 0)
  {
    return `+ $${Math.abs(amount).toLocaleString('en-US', {
        style: 'currency',
        currency: 'USD',
        minimumFractionDigits: 2,
      }).slice(1)}`; 
  } 
  else 
  {
    return `$${amount.toLocaleString('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumFractionDigits: 2,
    })}`;
  }
};


</script>
