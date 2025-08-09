<template>
  <div class="category-report">
    <h3>Category Report</h3>
    <div v-if="Object.keys(categoryTotals).length > 0">
      <ul>
        <li v-for="(total, category) in categoryTotals" :key="category">
          <strong>{{ category }}:</strong> {{ formatAmount(total) }}
        </li>
      </ul>
    </div>
    <p v-else>No transactions with categories yet.</p>
  </div>
</template>

<script setup>
import { defineProps, computed } from 'vue';

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const categoryTotals = computed(() => {
  const totals = {};
  props.transactions.forEach(transaction => {
    if (transaction.category) {
      if (!totals[transaction.category]) {
        totals[transaction.category] = 0;
      }
      totals[transaction.category] += transaction.amount;
    }
  });
  return totals;
});

const formatAmount = (amount) => {
  if (amount > 0) {
    return `+ $${amount.toLocaleString('en-US', {
      minimumFractionDigits: 2,
    })}`;
  } else if (amount < 0) {
    return `- $${Math.abs(amount).toLocaleString('en-US', {
      minimumFractionDigits: 2,
    })}`;
  } else {
    return `$${amount.toLocaleString('en-US', {
      minimumFractionDigits: 2,
    })}`;
  }
};
</script>

<style scoped>
.category-report {
  margin-top: 20px;
  padding: 15px;
  background-color: #f8f9fa;
  border-radius: 5px;
}

.category-report h3 {
  border-bottom: 1px solid #dee2e6;
  padding-bottom: 10px;
  margin-bottom: 15px;
}

.category-report ul {
  list-style: none;
  padding: 0;
}

.category-report li {
  padding: 5px 0;
  border-bottom: 1px dashed #dee2e6;
}

.category-report li:last-child {
  border-bottom: none;
}
</style>