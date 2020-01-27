<template>
  <div id="app">
    <b-container>
      <Budget v-bind:incomes="incomes" v-bind:expenses="expenses" v-bind:total="total" />
        <b-row>
          <b-col>
            <Income v-bind:incomes="incomes" v-bind:total="total" v-on:delete-income="deleteIncome" v-on:add-income="addIncome" />
          </b-col>
          <b-col>
            <Expenses v-bind:expenses="expenses" v-bind:total="total" v-on:delete-expense="deleteExpense" v-on:add-expense="addExpense" />
          </b-col>
        </b-row>
    </b-container>
  </div>
</template>

<script>

import Budget from "./components/Budget"
import Income from "./components/Income"
import Expenses from "./components/Expenses"
import Chartkick from "vue-chartkick"

export default {
  name: 'app',
  components: {
    Budget,
    Income,
    Expenses
  },
  data() {
    return {
      incomes: [
        {
          name: "Work",
          value: 1200
        },
        {
          name: "Extra",
          value: 230
        },
        {
          name: "Tips",
          value: 80
        }
      ],
      expenses: [
        {
          name: "Bills",
          value: 350
        },
        {
          name: "Food",
          value: 200
        },
        {
          name: "Savings",
          value: 400
        }
      ],
      total: {
        income: 0,
        expense: 0
      }
    }
  },
  mounted: function () {
    // Display the "income and expense" chart with our prefilled data
    const incomeSum = this.incomes
          .map(income => parseInt(income.value))
          .reduce((a, b) => a + b, 0);

    const expenseSum = this.expenses
          .map(expense => parseInt(expense.value))
          .reduce((a, b) => a + b, 0);

    this.total.income = incomeSum;
    this.total.expense = expenseSum;

    let barChart = Chartkick.charts["income-expense-chart"];
    barChart.updateData({
      "Monthly Income": incomeSum,
      "Monthly Expense": expenseSum
    })

    // Display the "overview donut" chart with our prefilled data
    const allExpenses = this.expenses.reduce(function(obj, item) {
        obj[item.name] = item.value;
        return obj;
    }, {})

    let donutChart = Chartkick.charts["overview-chart"];
    donutChart.updateData(allExpenses)
  },
  methods: {
    deleteIncome(value) {
        this.incomes = this.incomes.filter(income => income.value !== value);
        this.total.income -= value;
    },
    deleteExpense(value) {
        this.expenses = this.expenses.filter(expense => expense.value !== value);
        this.total.expense -= value;
    },
    addIncome() {
      // Get the income name and value and store them into the array
      let name = this.incomes.name;
      let value = this.incomes.value;

      if(name.length && value > 0) {
          this.incomes = [...this.incomes, { name, value }]

          // Add up all incomes
          this.total.income += value;

          // Clear the inputs
          this.name = "";
          this.value = "";
      }
    },
    addExpense() {
      // Get the expense name and value and store them into the array
      let name = this.expenses.name;
      let value = this.expenses.value;

      if(name.length && value > 0) {
          this.expenses = [...this.expenses, { name, value }]

          // Add up all expenses
          this.total.expense += value;

          // Clear the inputs
          this.name = "";
          this.value = "";
      }
    }
  }
}

</script>

<style>
  body {
    font-family: 'Exo', sans-serif !important;
  }
  input {
        width: 250px;
        padding: 5px;
    }
  h4 {
    color: #B6839E;
    font-weight: 600 !important;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
</style>
