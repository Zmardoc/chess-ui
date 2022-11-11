<template>
  <main>
    <section role="region" aria-label="Board Controls">
      <button type="button" @click="toggleOrientation">
        Toggle orientation
      </button>
      <button type="button" @click="resetBoard">Reset</button>
    </section>
    <TheChessboard
      :board-config="boardConfig"
      @board-created="(api) => (boardAPI = api)"
      @checkmate="handleCheckmate"
    />
  </main>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { TheChessboard } from 'vue3-chessboard'
import 'vue3-chessboard/style.css'
import type { ChessboardAPI, BoardConfig } from 'vue3-chessboard'

const boardAPI = ref<ChessboardAPI>()
const boardConfig: BoardConfig = {
  coordinates: false,
  autoCastle: false,
}

function handleCheckmate(isMated: string) {
  if (isMated === 'w') {
    alert('Black wins!')
  } else {
    alert('White wins!')
  }
}

function toggleOrientation() {
  boardAPI.value?.board.toggleOrientation()
}

function resetBoard() {
  if (boardAPI.value) {
    console.log(boardAPI.value.game.fen())
  }

  boardAPI.value?.resetBoard()
}
</script>
