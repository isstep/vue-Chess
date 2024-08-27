<template>
  <img :src="pieceSrc" :alt="piece" class="w-full h-full object-contain" />
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  piece: String
});

const pieceSrc = computed(() => {
  const basePath = '/pieces/';
  const pieceMap = {
    'P': `${basePath}Piece=Pawn, Side=White.png`,
    'N': `${basePath}Piece=King, Side=White.png`,
    'R': `${basePath}Piece=Rook, Side=White.png`,
    'B': `${basePath}Piece=Bishop, Side=White.png`,
    'Q': `${basePath}Piece=Queen, Side=White.png`,
    'K': `${basePath}Piece=King, Side=White.png`,

    'p': `${basePath}Piece=Pawn, Side=Black.png`,
    'r': `${basePath}Piece=Rook, Side=Black.png`,
    'n': `${basePath}Piece=Knight, Side=Black.png`,
    'b': `${basePath}Piece=Bishop, Side=Black.png`,
    'q': `${basePath}Piece=Queen, Side=Black.png`,
    'k': `${basePath}Piece=King, Side=Black.png`
  };
  
  return pieceMap[props.piece] || '';
});
</script>
