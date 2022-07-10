<template>
  <p>{{ timerDisplay }}</p>

  <form action="">
    <label for="Mins">Seconds</label>
    <input v-model="state.timers.seconds" id="Secs" />
    <label for="Seconds">minutes</label>
    <input v-model="state.timers.minutes" id="Mins" />
  </form>

  <button @click='startTimer' :disabled='state.startDisabled'>Start</button>
  <button @click='stopTimer(interval)'>Stop</button>

</template>

<script setup>
import { reactive, ref } from "vue";

    const state = reactive({ timers: { seconds: 0, minutes: 0, timer: 0 }, interval: 0, startDisabled: false });
    const timerLimit = ref(0);
    const timerDisplay = ref(0)

    function startTimer() {
      state.startDisabled = true;

      var start = Date.now();

      console.log("input is: " + state.timers.minutes + " minutes " + state.timers.seconds + " seconds");

      var end = start + (state.timers.minutes * 60 * 1000) + (state.timers.seconds * 1000);


      state.interval = setInterval(function () {
        timerLimit.value = Date.now();

        timerDisplay.value = ((end - timerLimit.value)/1000).toFixed(2);

        state.timer = timerLimit.value;

        if (timerLimit.value >= end) {
          clearInterval(state.interval);
          console.log(Date.now()-end)
          state.startDisabled = false;
          timerDisplay.value ="Complete";
        }
      }, 1);
    }

    function stopTimer() {
      clearInterval(state.interval);
      state.startDisabled = false;
    }
</script>

<style></style>
