<template>
    <h3>Add new transaction</h3>
    <form id="form">
        <div class="form-control">
            <label for="text">Text</label>
            <input type="text" id="text" placeholder="Enter text..." v-model="name"/>
        </div>
        <div class="form-control">
            <label for="amount"
            >Amount <br />
            (negative - expense, positive - income)</label
            >
            <input type="number" id="amount" placeholder="Enter amount..." v-model="amount"/>
        </div>
        <button class="btn" @click="onSubmit">Add transaction</button>
    </form>
</template>

<script setup>
    import { useToast } from "vue-toastification";
    import { ref, defineEmits } from "vue";

    const name = ref('');
    const amount = ref('');
    const emit = defineEmits(["transactionSubmitted"]);

    const toast = useToast();

    const onSubmit = (e) => {
        e.preventDefault();

        if (!name.value || !amount.value) {
            toast.error('Fields are required.');
        } else {
            toast.success('Just a toast');
        }
        
        emit("transactionSubmitted", {
            id: generateUniqueId(),
            name: name.value,
            amount: amount.value,

        })
    }

    const generateUniqueId = () => {
        return Math.floor(Math.random() * 1000000);
    }
</script>