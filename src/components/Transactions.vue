<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus' ">
            {{transaction.name}} <span>{{ transaction.amount < 0 ? '-' : ''}}${{ Math.abs(transaction.amount) }}</span><button class="delete-btn" @click="handleDeleteTransaction(transaction.id)">x</button>
        </li>
    </ul>
</template>

<script setup>
    import { defineProps, defineEmits } from 'vue';

    const props = defineProps({
        transactions: {
            type: Array,
            required: true
        }
    });

    const emits = defineEmits(['deleteTransaction']);

    const handleDeleteTransaction = (id) => {
        emits('deleteTransaction', id);
    }
</script>