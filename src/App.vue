<template>
  <!-- outer most box -->
  <div class="w-screen h-screen flex justify-center items-center">
    <!-- main card -->
    <div class="w-[700px] rounded-md border border-solid border-black p-4 space-y-4">
      <!-- balance card -->
      <div class="grow rounded-md border border-solid border-black divide-y divide-black">
        <div class="grow p-4">Balance</div>
        <div class="grow flex divide-x divide-black">
          <div class="grow p-4">Income</div>
          <div class="grow p-4">Expenses</div>
        </div>
      </div>
      <!-- inputs -->
      <div class="flex space-x-4">
        <input
          type="text"
          name="Description"
          id="email"
          class="grow rounded-md border-0 py-1.5 text-gray-900 p-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
          placeholder="Description"
        />
        <input
          type="text"
          name="Amount"
          id="email"
          class="grow rounded-md border-0 py-1.5 text-gray-900 p-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
          placeholder="Amount"
        />
        <button
          type="button"
          class="rounded-md bg-indigo-600 px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          Add Transaction
        </button>
      </div>
      <!-- Table import table component-->
      <Table />
    </div>
  </div>
</template>

<script lang="ts" setup>
import Table from './components/Table.vue'
</script>
