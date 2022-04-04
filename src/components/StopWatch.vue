<template>
  <p>{{ state.timer }}</p>
  <button @click="startTimer">Start</button>
  <button @click="stopTimer(state.interval)">Stop</button>
</template>

<script>
import { reactive } from "vue";

export default {
  setup() {
    const state = reactive({ timer: 12 }, { timeLimit: 5 }, { interval: "" });

    function startTimer() {
      state.interval = setInterval(() => {
        if (this.timer == 0) {
          clearInterval(this.in);
        } else {
          state.timer--;
        }
      }, 1000);
    }

    function stopTimer(interval) {
      clearInterval(interval);
    }
    function convertToTime(seconds) {
      console.log(seconds);
    }
    return {
      state,
      startTimer,
      stopTimer,
    };
  },
};
</script>

<style></style>
