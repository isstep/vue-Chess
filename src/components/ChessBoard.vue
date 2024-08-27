<script setup>
import { reactive } from 'vue';
import ChessPiece from './ChessPiece.vue';

const initialBoard = [
  'r', 'n', 'b', 'q', 'k', 'b', 'n', 'r',
  'p', 'p', 'p', 'p', 'p', 'p', 'p', 'p',
  '', '', '', '', '', '', '', '',
  '', '', '', '', '', '', '', '',
  '', '', '', '', '', '', '', '',
  '', '', '', '', '', '', '', '',
  'P', 'P', 'P', 'P', 'P', 'P', 'P', 'P',
  'R', 'N', 'B', 'Q', 'K', 'B', 'N', 'R'
];

const state = reactive({
  board: [...initialBoard], 
  selectedPieceIndex: null,
  currentPlayer: 'white'
});

function getSquareClasses(index) {
  const row = Math.floor(index / 8);
  const isEvenRow = row % 2 === 0;
  const isEvenIndex = index % 2 === 0;
  return isEvenRow
    ? isEvenIndex ? 'bg-gray-300' : 'bg-gray-700'
    : isEvenIndex ? 'bg-gray-700' : 'bg-gray-300';
}

function selectSquare(index) {
  if (state.selectedPieceIndex === null) {
    const piece = state.board[index];
    if (piece && isCorrectPlayerPiece(piece)) {
      state.selectedPieceIndex = index;
    }
  } else {
    movePiece(state.selectedPieceIndex, index);
    state.selectedPieceIndex = null;
  }
}

function movePiece(from, to) {
  state.board[to] = state.board[from];
  state.board[from] = '';
  switchPlayer();
}

function switchPlayer() {
  state.currentPlayer = state.currentPlayer === 'white' ? 'black' : 'white';
}

function isCorrectPlayerPiece(piece) {
  return state.currentPlayer === 'white' ? piece === piece.toUpperCase() : piece === piece.toLowerCase();
}
</script>

<template>
  <div class="grid grid-cols-8 grid-rows-8 w-96 h-96 border-2 border-gray-600">
    <div
      v-for="(square, index) in state.board"
      :key="index"
      :class="getSquareClasses(index)"
      @click="selectSquare(index)"
      class="flex justify-center items-center"
    >
      <ChessPiece
        v-if="square"
        :piece="square"
      />
    </div>
  </div>
</template>
