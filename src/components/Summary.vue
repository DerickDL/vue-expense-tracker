<template>
    <div class="inc-exp-container">
        <div>
            <h4>Income</h4>
            <p id="money-plus" class="money plus">+${{ totalIncome }}</p>
        </div>
        <div>
            <h4>Expense</h4>
            <p id="money-minus" class="money minus">-${{ Math.abs(totalExpenses) }}</p>
        </div>
    </div>
</template>

<script setup>

    import { defineProps } from 'vue';

    const props = defineProps({
        totalIncome: {
            type: Number,
            required: true
        },
        totalExpenses: {
            type: Number,
            required: true
        }
    });

</script>