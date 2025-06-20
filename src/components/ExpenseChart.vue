<!-- src/components/ExpenseChart.vue -->
<template>
  <div>
    <Pie :data="chartData" :options="chartOptions" />
  </div>
</template>

<script>
import { Pie } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  ArcElement
} from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, ArcElement)

export default {
  name: 'ExpenseChart',
  components: { Pie },
  props: ['expenses'],
  computed: {
    chartData() {
      const totals = {}
      this.expenses.forEach(exp => {
        const cat = exp.category
        totals[cat] = (totals[cat] || 0) + parseFloat(exp.amount)
      })

      return {
        labels: Object.keys(totals),
        datasets: [
          {
            label: 'Expenses by Category',
            data: Object.values(totals),
            backgroundColor: ['#6366F1', '#10B981', '#F59E0B', '#EF4444']
          }
        ]
      }
    },
    chartOptions() {
      return {
        responsive: true,
        plugins: {
          legend: {
            position: 'top'
          },
          title: {
            display: true,
            text: 'Expense Distribution'
          }
        }
      }
    }
  }
}
</script>

<style scoped>
div {
  max-width: 500px;
  margin: auto;
}
</style>
