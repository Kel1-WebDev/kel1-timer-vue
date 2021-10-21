<template>
  <div>
    <div class="container">
      <h1 name class="name dark-blue">WebDev Teori</h1>
      <img delete class="del-btn" src="../assets/delete.svg" />
    </div>
    <div>
      <div class="blabla">
        <p time class="time">{{ formatTime(time) }}</p>
        <div class="container">
          <img start class="timer-btn" v-bind:src="startButton" @click="start()" />
          <img
            stop
            class="timer-btn dark-blue"
            src="../assets/stop.svg"
            @click="stop()"
          />
        </div>
      </div>
    </div>
    <div>
      <div history class="history">
        <button showHistory class="accordion"><span> ▶ </span> History</button>
        <div historyList class="history-list"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "StopwatchItem",
  data: function () {
    return {
      time: 0,
      state: "stop",
      interval: null,
      startButton: require("../assets/play.svg"),
    };
  },
  methods: {
    insertZero(time) {
      if (time < 10) return "0" + time;
      return time;
    },
    formatTime(second) {
      let divisor = 60 * 60;

      const hour = Math.floor(second / divisor);
      second = second % divisor;
      divisor = divisor / 60;

      const minute = Math.floor(second / divisor);
      second = second % divisor;

      return (
        this.insertZero(hour) +
        ":" +
        this.insertZero(minute) +
        ":" +
        this.insertZero(second)
      );
    },
    incrementTime() {
      this.time++;
    },
    start() {
      if (this.state === "pause" || this.state === "stop") {
        this.state = "start";
        this.interval = setInterval(this.incrementTime, 1000);

        this.startButton = require("../assets/pause.svg");
      } else if (this.state === "start") {
        this.state = "pause";
        clearInterval(this.interval);

        this.startButton = require("../assets/play.svg");
      }
    },
    stop() {
      this.state = "stop";
      clearInterval(this.interval);
      this.time = 0;
    },
  },
};
</script>

<style scoped>
@import url("../styles/timer.css");
@import url("../styles/history.css");
</style>
