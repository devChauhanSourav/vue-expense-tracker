<template>
  <main class="min-h-screen bg-gray-50 p-6">
    <div class="max-w-2xl mx-auto bg-white shadow p-6 rounded-xl">
      <h1 class="text-2xl font-bold text-indigo-600 mb-4">💰 Expense Tracker</h1>

      <ExpenseForm @add-expense="addExpense" />
      <FilterBar @filter-change="updateFilters" />
      <ExpenseList :expenses="filteredExpenses" />
      <ExpenseChart :expenses="filteredExpenses" />

    </div>
  </main>
</template>


<script>
import { ref, onMounted, computed } from 'vue'
import ExpenseForm from './components/ExpenseForm.vue'
import FilterBar from './components/FilterBar.vue'
import ExpenseList from './components/ExpenseList.vue'
import ExpenseChart from './components/ExpenseChart.vue'


export default {
  components: { ExpenseForm, FilterBar, ExpenseList, ExpenseChart },
  setup() {
    const expenses = ref([])
    const filters = ref({ category: '', startDate: '', endDate: '' })

    const updateFilters = (newFilters) => {
      filters.value = newFilters
    }

    const addExpense = (expense) => {
      expense.id = Date.now()
      expenses.value.push(expense)
      localStorage.setItem('expenses', JSON.stringify(expenses.value))
    }

const filteredExpenses = computed(() => {
  return expenses.value.filter((exp) => {
    const expDate = new Date(exp.date)
    const startDate = filters.value.startDate ? new Date(filters.value.startDate) : null
    const endDate = filters.value.endDate ? new Date(filters.value.endDate) : null

    const matchCategory =
      !filters.value.category || exp.category.toLowerCase() === filters.value.category.toLowerCase()

    const matchStart = !startDate || expDate >= startDate
    const matchEnd = !endDate || expDate <= endDate

    return matchCategory && matchStart && matchEnd
  })
})



    onMounted(() => {
      const saved = localStorage.getItem('expenses')
      if (saved) {
        expenses.value = JSON.parse(saved)
      }
    })

    return {
      expenses,
      filteredExpenses,
      addExpense,
      updateFilters,
    }
  },
}
</script>

