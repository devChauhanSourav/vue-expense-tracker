<template>
  <form @submit.prevent="submitExpense" class="space-y-4">
    <input
      v-model="title"
      type="text"
      placeholder="Expense Title"
      class="w-full px-4 py-2 border rounded-lg"
      required
    />

    <input
      v-model.number="amount"
      type="number"
      placeholder="Amount"
      class="w-full px-4 py-2 border rounded-lg"
      required
    />

    <select v-model="category" class="w-full px-4 py-2 border rounded-lg">
      <option disabled value="">Select category</option>
      <option value="Food">🍔 Food</option>
      <option value="Bills">💡 Bills</option>
      <option value="Travel">🚗 Travel</option>
    </select>

    <button type="submit" class="bg-indigo-600 text-white px-4 py-2 rounded-lg hover:bg-indigo-700">
      Add Expense
    </button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      amount: '',
      category: '',
    }
  },
  methods: {
    submitExpense() {
      const newExpense = {
        id: Date.now(),
        title: this.title,
        amount: this.amount,
        category: this.category,
        date: new Date().toISOString().slice(0, 10),
      }
      this.$emit('add-expense', {
        title: this.title,
        amount: this.amount,
        category: this.category,
        date: this.date,
      })


      // Reset
      this.title = ''
      this.amount = ''
      this.category = ''
    },
  },
}
</script>
