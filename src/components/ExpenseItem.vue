<template>
  <div class="flex justify-between items-center bg-gray-100 px-4 py-2 rounded">
    <div>
      <h3 class="font-semibold">{{ expense.title }}</h3>
      <p class="text-sm text-gray-500">{{ expense.category }} • {{ expense.date }}</p>
    </div>
    <div class="text-indigo-600 font-semibold">₹{{ expense.amount }}</div>
  </div>
</template>

<script>
export default {
  props: {
    expense: {
      type: Object,
      required: true,
    },
  },
}
</script>
