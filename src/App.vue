<template>
  <div class="w-screen h-screen flex justify-center items-center">
    <div class="flex-col space-y-4">
      <Select v-model="selectedPeice" />
      <div class="flex-col">
        <div v-for="y in 8" :key="y" class="flex">
          <div
            v-for="x in 8"
            :key="x"
            style="width: 100px; height: 100px"
            :style="
              selectedCell?.x === x && selectedCell?.y === y
                ? 'background: red'
                : validMoves.some((move) => move.x === x && move.y === y)
                  ? 'background: lightgreen'
                  : ''
            "
            class="flex items-center justify-center p-4 border border-solid border-black"
            @click="handleCellClick(x, y)"
          >
            x: {{ x }}, y: {{ y }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'
import Select from './components/Select.vue'

interface Coordinate {
  x: number
  y: number
}

const selectedPeice = ref('Soldier')
const selectedCell = ref<Coordinate>({ x: 0, y: 0 })
const validMoves = ref<Coordinate[]>([])

const handleCellClick = (x: number, y: number) => {
  selectedCell.value = { x, y }
  const soldierMoves = [{ x, y: y + 1 }]
  const kingMoves = [
    { x, y: y + 1 },
    { x, y: y - 1 },
    { x: x - 1, y },
    { x: x + 1, y },
    { x: x - 1, y: y - 1 },
    { x: x + 1, y: y + 1 },
    { x: x + 1, y: y - 1 },
    { x: x - 1, y: y + 1 }
  ]

  switch (selectedPeice.value) {
    case 'Soldier':
      validMoves.value = soldierMoves
      break
    case 'King':
      validMoves.value = kingMoves
      break
    default:
      validMoves.value = []
      break
  }
}

watch(selectedPeice, () => {
  validMoves.value = []
  selectedCell.value = { x: 0, y: 0 }
})
</script>
