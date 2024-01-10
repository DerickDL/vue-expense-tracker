<template>
    <Header />
    <div class="container">
        <Balance :totalBalance="totalBalance"/>
        <Summary :totalIncome="+totalIncome" :totalExpenses="+totalExpenses" />
        <Transactions :transactions="transactions" @deleteTransaction="handleDeleteTransaction"/>
        <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
    </div>
</template>

<script setup>
    import Header from "./components/Header.vue";
    import Balance from "./components/Balance.vue";
    import Summary from "./components/Summary.vue";
    import Transactions from "./components/Transactions.vue";
    import AddTransaction from "./components/AddTransaction.vue";
    import { ref, onMounted, computed } from "vue";


    const transactions = ref([]);

    onMounted(() => {
        transactions.value = [
            {id: 1, name: "Paycheck", amount: 1000},
            {id: 2, name: "Commission", amount: 750},
            {id: 3, name: "House Mortgage", amount: -250},
            {id: 4, name: "Car Ammortization", amount: -250}
        ];
    });

    const totalBalance = computed(() => {
        return transactions.value.reduce((acc, transaction) => acc + transaction.amount, 0)
    })

    const totalIncome = computed(() => {
        return transactions.value
            .filter(transaction => transaction.amount > 0)
            .reduce((acc, transaction) => acc + transaction.amount, 0)
            .toFixed(2)
    })

    const totalExpenses = computed(() => {
        return transactions.value
            .filter(transaction => transaction.amount < 0)
            .reduce((acc, transaction) => acc + transaction.amount, 0)
            .toFixed(2)
    })

    const handleTransactionSubmitted = (transactionData) => {
        transactions.value.push({
            ...transactionData
        });
    }

    const handleDeleteTransaction = (transactionId) => {
        const filteredTransactions =  transactions.value.filter(transaction => transaction.id !== transactionId);
        transactions.value = filteredTransactions;
    }
    
</script>