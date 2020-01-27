<template>
    <div>
        <h2>Expenses:</h2>
        <ul>
            <li v-for="expense in expenses" v-bind:key="expense.value">
                {{ expense.name }}: ${{ expense.value }}
                <b-button v-on:click="$emit('delete-expense', expense.value)">x</b-button>
            </li>
        </ul>
        <b-button v-b-modal.modal-2>Add New Expense</b-button>
        <b-modal v-on:ok="$emit('add-expense')" id="modal-2" title="Add Expense" ok-only>
            <span>Expense Name: </span>
            <input type="text" v-model="expenses.name" />
            <br />
            <span>Expense Value: </span>
            <input type="number" v-model.number="expenses.value" />
        </b-modal>
        <hr />
        <span>Total Monthly: ${{ total.expense }}</span>
    </div>
</template>

<script>

export default {
    name: "Expenses",
    props: ["expenses", "total"]
}

</script>

<style scoped>
    h2 {
        background: #A199B6;
        color: #ffffff;
        font-style: italic;
        padding: 10px 0;
        text-align: center;
        margin: 40px 0;
    }
</style>