<template>
  <div id="app">
    <board />
  </div>
</template>

<script>
import Board from "./components/Board.vue";
export default {
  name: "app",
  components: {
    Board,
  },
};
</script>
