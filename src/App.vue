<template>
  <!-- outer most box -->
  <div class="w-screen h-screen flex justify-center items-center">
    <!-- main card -->
    <div class="w-[700px] rounded-md border border-solid border-black p-4 space-y-4">
      <!-- balance card -->
      <div class="grow rounded-md border border-solid border-black divide-y divide-black">
        <div class="grow p-4">Balance: {{ income + expenses }}</div>
        <div class="grow flex divide-x divide-black">
          <div class="grow p-4">Income: {{ income }}</div>
          <div class="grow p-4">Expenses: {{ expenses }}</div>
        </div>
      </div>
      <!-- inputs -->
      <div class="flex space-x-4">
        <input
          v-model="transactionFormData.description"
          type="text"
          name="Description"
          id="email"
          class="grow rounded-md border-0 py-1.5 text-gray-900 p-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
          placeholder="Description"
        />
        <input
          v-model="transactionFormData.amount"
          type="number"
          name="Amount"
          id="email"
          class="grow rounded-md border-0 py-1.5 text-gray-900 p-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
          placeholder="Amount"
        />
        <button
          type="button"
          class="rounded-md bg-indigo-600 px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          @click="addTransaction"
        >
          Add Transaction
        </button>
      </div>
      <!-- Table import table component-->
      <Table
        :transactionsList="transactions"
        @deleteTransaction="
          (index) => {
            deleteTransaction(index)
          }
        "
      />
    </div>
  </div>
</template>

<script lang="ts" setup>
import { computed, ref } from 'vue'
import Table from './components/Table.vue'

const transactionFormData = ref({
  description: '',
  amount: 0
})

const transactions = ref([
  {
    description: 'Coffee',
    amount: 100
  },
  {
    description: 'Chai',
    amount: -100
  }
])

const income = computed(() => {
  let sum = 0
  transactions.value.forEach((transaction) => {
    if (transaction.amount >= 0) {
      sum = sum + transaction.amount
    }
  })
  return sum
})
const expenses = computed(() => {
  let sum = 0
  transactions.value.forEach((transaction) => {
    if (transaction.amount < 0) {
      sum = sum + transaction.amount
    }
  })
  return sum
})

const addTransaction = () => {
  transactions.value.push({ ...transactionFormData.value })
}

const deleteTransaction = (index: number) => {
  transactions.value.splice(index, 1)
}
</script>
