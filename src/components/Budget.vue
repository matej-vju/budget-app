<template>
    <div>
        <h2>Budget</h2>
        <b-row align-v="center" align-h="center">
            <b-col>
                <FlexSpending v-bind:total="total" />
            </b-col>
            <b-col>
                <IncomeOutcomeChart v-bind:incomes="incomes" v-bind:expenses="expenses" v-bind:total="total" />
            </b-col>
            <b-col>
                <OverviewChart v-bind:expenses="expenses" />
            </b-col>
        </b-row>
    </div>
</template>

<script>

import FlexSpending from "./charts/FlexSpending"
import IncomeOutcomeChart from "./charts/IncomeOutcomeChart"
import OverviewChart from "./charts/OverviewChart"

export default {
    name: "Budget",
    components: {
        FlexSpending,
        IncomeOutcomeChart,
        OverviewChart
    },
    props: ["incomes", "expenses", "total"],
}
</script>

<style scoped>
    h2 {
        background: #80A4AD;
        color: #ffffff;
        font-style: italic;
        padding: 10px 0;
        text-align: center;
        margin-bottom: 50px;
    }
</style>