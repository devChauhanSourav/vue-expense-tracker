<template>
  <div class="flex gap-4 mb-4 flex-wrap">
    <select v-model="category" class="border rounded p-2">
      <option value="">All Categories</option>
      <option value="food">Food</option>
      <option value="travel">Travel</option>
      <option value="bills">Bills</option>
    </select>

    <input type="date" v-model="startDate" class="border rounded p-2" />
    <input type="date" v-model="endDate" class="border rounded p-2" />

    <button @click="applyFilters" class="bg-indigo-600 text-white px-4 py-2 rounded">
      Apply
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      category: '',
      startDate: '',
      endDate: '',
    }
  },
  methods: {
    applyFilters() {
      this.$emit('filter-change', {
        category: this.category,
        startDate: this.startDate,
        endDate: this.endDate,
      })
    },
  },
}
</script>
