<template>
  <div>
    <Header />
    <div class="container p-5">
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
     
      
      <TransactionList
        :transactions="transactions"
        @transactionDeleted="handleTransactionDeleted"
      />

      <IncomeExpenses :income="income" :expenses="expenses" />

      
      <Balance :total="total" />
      
    </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import AddTransaction from './components/AddTransaction.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';

import { ref, computed, onMounted } from 'vue';
import { useToast } from 'vue-toastification';

const toast = useToast();

// Define reactive variables
const transactions = ref([]);

// Fetch transactions from localStorage on component mount
onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

// Compute total balance
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => acc + transaction.amount, 0);
});

// Compute total income
const income = computed(() => {
  return transactions.value
    .filter(transaction => transaction.amount > 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});

// Compute total expenses
const expenses = computed(() => {
  return transactions.value
    .filter(transaction => transaction.amount < 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});

// Handle transaction submission
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });

  saveTransactionsToLocalStorage();

  toast.success('Transaction added.');
};

// Generate unique ID for transactions
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

// Handle transaction deletion
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter(transaction => transaction.id !== id);

  saveTransactionsToLocalStorage();

  toast.success('Transaction deleted.');
};

// Save transactions to localStorage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
};
</script>
