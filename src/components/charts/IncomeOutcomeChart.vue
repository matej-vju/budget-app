<template>
    <div>
        <column-chart id="income-expense-chart" width="300px" />
    </div>
</template>

<script>

import Chartkick from 'vue-chartkick'

export default {
    name: "IncomeOutcomeChart",
    props: ["incomes", "expenses", "total"],

    // Watch a computed value of incomes and expenses
    computed: {
        combined() {
            return this.incomes && this.expenses
        }
    },

    // Watch for the "combined" changes and update the bar chart accordingly
    watch: {
        combined: function() {
            const incomeSum = this.incomes
                .map(income => parseInt(income.value))
                .reduce((a, b) => a + b, 0);

            const expenseSum = this.expenses
                .map(expense => parseInt(expense.value))
                .reduce((a, b) => a + b, 0);

            let chart = Chartkick.charts["income-expense-chart"];
            chart.updateData({
                "Monthly Income": incomeSum,
                "Monthly Expense": expenseSum
            })
        }
    }
}

</script>

<style scoped>

</style>