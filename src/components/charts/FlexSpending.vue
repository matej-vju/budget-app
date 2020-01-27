<template>
    <div class="flex-spending">
        <h4>Monthly Flex Spending</h4>
        <p>${{ (this.total.income - this.total.expense).toFixed(2) }}</p>
        <h4>Weekly</h4>
        <p>${{ ((this.total.income - this.total.expense) / 4).toFixed(2) }}</p>
        <h4>Daily</h4>
        <p>${{ ((this.total.income - this.total.expense) / 30).toFixed(2) }}</p>
    </div>
</template>

<script>

export default {
    name: "FlexSpending",
    props: ["total"]
}
</script>

<style scoped>
    .flex-spending {
        text-align: center;
    }
</style>