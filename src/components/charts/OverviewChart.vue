<template>
    <div>
        <pie-chart id="overview-chart" :donut="true" legend="bottom"></pie-chart>
    </div>
</template>

<script>

import Chartkick from "vue-chartkick"

export default {
    name: "OverviewChart",
    props: ["expenses"],

    // Watch for the "expenses" changes and update the donut chart accordingly
    watch: {
        expenses: function() {
            const result = this.expenses.reduce(function(obj, item) {
                obj[item.name] = item.value;
                return obj;
            }, {})

            let donutChart = Chartkick.charts["overview-chart"];
            donutChart.updateData(result)
        }
    }
}

</script>

<style scoped>
    #overview-chart {
        margin: 20px 0;
    }
</style>