<template>
  <div>
    <h4 class="text-center">Your Balance</h4>
    <h1 class="text-center" id="balance">{{ formatBalance(total) }}</h1>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  total: {
    type: Number,
    required: true,
  },
});

const formatBalance = (balance) => {
  if (balance > 0) {
    return `+ $${balance.toLocaleString('en-US', {
      minimumFractionDigits: 2,
    })}`;
  } else {
    return `- $${Math.abs(balance).toLocaleString('en-US', {
      minimumFractionDigits: 2,
    })}`;
  }
};
</script>
