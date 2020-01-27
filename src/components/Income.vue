<template>
    <div>
        <h2>Incomes:</h2>
        <ul>
            <li v-for="income in incomes" v-bind:key="income.value">
                {{ income.name }}: ${{ income.value }}
                <b-button variant="outline-danger" v-on:click="$emit('delete-income', income.value)">x</b-button>
            </li>
        </ul>
        <b-button v-b-modal.modal-1>Add New Income</b-button>
        <b-modal v-on:ok="$emit('add-income')" id="modal-1" title="Add Income" ok-only>
            <span>Income Name: </span>
            <input type="text" v-model="incomes.name" />
            <br />
            <span>Income Value: </span>
            <input type="number" v-model.number="incomes.value" />
        </b-modal>
        <hr />
        <span>Total Monthly: ${{ total.income }}</span>
    </div>
</template>

<script>

export default {
    name: "Income",
    props: ["incomes", "total"]
}

</script>

<style scoped>
    h2 {
        background: #9B5277;
        color: #ffffff;
        font-style: italic;
        padding: 10px 0;
        text-align: center;
        margin: 40px 0;
    }
</style>