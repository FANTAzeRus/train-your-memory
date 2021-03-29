<template>
  <div class="game">
    <div class="title">Игра "Тренируй свою память".</div>
    <div class="board">
      <div class="cell" v-for="(cell, idx) in state.cells" :key="`cell_${idx}`">
        {{ cell.value }}
      </div>
    </div>
  </div>
</template>

<script>
import "./styles/index.scss";
import { baseConstatnts, cellStateConst, gameStateConst } from "./constants";
import { reactive } from "@vue/reactivity";
import { onBeforeMount } from "@vue/runtime-core";

export default {
  name: "App",
  components: {},
  setup() {
    const state = reactive({
      cells: [],
      gameStatus: gameStateConst.stop,
    });
    const init = () => {
      clearCells();
    };
    const randomizer = (min, max) => {
      return Math.round(min - 0.5 + Math.random() * (max - min + 1));
    };
    const clearCells = () => {
      state.cells = [];
      for (let i = 0; i < baseConstatnts.cellsCount; i++) {
        state.cells.push({
          id: i,
          state: cellStateConst.empty,
          value: 0,
        });
      }
    };
    const prepareCells = () => {
      const half = baseConstatnts.cellsCount / 2;
      for (let i = 0; i < half; i++) {
        for (let j = 0; j < 2; j++) {
          let idx = randomizer(0, baseConstatnts.cellsCount - 1);

          if (state.cells[idx].value === 0) {
            state.cells[idx].state = cellStateConst.set;
            state.cells[idx].value = i + 1;
          } else {
            j--;
          }
        }
      }
    };

    onBeforeMount(() => {
      init();
      prepareCells();
    });

    return { state };
  },
};
</script>