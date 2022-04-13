<template>
  <p>{{ state.timer }}</p>
  <button @click="startTimer">Start</button>
  <button @click="stopTimer(interval)">Stop</button>
  <form action="">
    <label for="Mins">Seconds</label>
    <input v-model="state.timers.timer" id="Mins" />
    <label for="Seceonds">Seconds</label>
  </form>
</template>

<script>
import { reactive, ref } from "vue";

export default {
  setup() {
    const state = reactive({ timers: { timer: 0 }, interval: 0, startEnabled: true });
    const timerLimit = ref(0);

    function startTimer() {
      state.startEnabled = false;
      var start = Date.now();

      console.log("input is: " + state.timers.timer);
      var end = start + state.timers.timer * 1000;
      // console.log(start);

      state.interval = setInterval(function () {
        var delta = Date.now();

        console.log("now: " + delta);
        console.log("end: " + end);

        if (delta >= end) {
          clearInterval(state.interval);
          state.startEnabled = true;
          console.log("Complete");
        }
      }, 10);
    }

    function stopTimer() {
      clearInterval(state.interval);
      state.startEnabled = true;
    }
    return {
      state,
      startTimer,
      stopTimer,
      timerLimit,
    };
  },
};
</script>

<style></style>
