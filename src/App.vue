<template>
  <div class="game">
    Игра "Тренируй свою память".
    <div class="board">
      <div
        class="cell"
        v-for="(cell, idx) in baseConstatnts.cellsCount"
        :key="`cell_${idx}`"
      ></div>
    </div>
  </div>
</template>

<script>
import "./styles/index.scss";
import { baseConstatnts } from "./constants";

export default {
  name: "App",
  components: {},
  setup() {
    return { baseConstatnts };
  },
};
</script>