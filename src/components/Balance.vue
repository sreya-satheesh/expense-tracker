<template>
  <div class="mt-3">
    <p class="text-left"><strong>Balance :</strong> <span id="balance">{{ formatBalance(total) }}</span></p>
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
  } else if (balance < 0) {
    // Adjusting the formatting for negative balances
    return `- $${Math.abs(balance).toLocaleString('en-US', {
      minimumFractionDigits: 2,
    })}`;
  } else {
    return `$${balance.toLocaleString('en-US', {
      minimumFractionDigits: 2,
    })}`;
  }
};
</script>
