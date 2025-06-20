<template>
  <div class="mt-6 space-y-2">
    <ExpenseItem
      v-for="expense in expenses"
      :key="expense.id"
      :expense="expense"
    />
  </div>
</template>

<script>
import ExpenseItem from './ExpenseItem.vue'

export default {
  components: { ExpenseItem },
  props: ['expenses'],
}
</script>
