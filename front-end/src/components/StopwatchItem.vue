<template>
  <div>
    <div class="container">
      <h1 name class="name dark-blue">{{ name }}</h1>
      <img
        delete
        class="del-btn"
        src="../assets/delete.svg"
        @click="$emit('remove', this.id)"
      />
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
        <button @click="toggleHistory()" class="accordion">
          <span v-if="isHistoryShown"> ▼ </span>
          <span v-else> ▶ </span> History
        </button>
        <div v-if="isHistoryShown" class="history-list">
          <li v-for="(item, index) in histories" :key="index">
            <span>{{ formatTime(item) }}</span>
          </li>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "StopwatchItem",
  props: {
    id: {
      type: Number,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    time: {
      type: Number,
      required: true,
    },
    state: {
      type: String,
      required: true,
    },
  },
  data: function () {
    return {
      interval: null,
      startButton: require("../assets/play.svg"),
      histories: [],
      isHistoryShown: false,
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
      this.$emit("updateTime", this.id, this.time + 1);
    },
    start() {
      if (this.state === "pause" || this.state === "stop") {
        this.$emit("updateState", this.id, "start");
        this.interval = setInterval(this.incrementTime, 1000);

        this.startButton = require("../assets/pause.svg");
      } else if (this.state === "start") {
        this.$emit("updateState", this.id, "pause");
        clearInterval(this.interval);

        this.startButton = require("../assets/play.svg");
      }
    },
    stop() {
      this.$emit("updateState", this.id, "stop");
      clearInterval(this.interval);

      if (this.time > 0) {
        this.histories.push(this.time);
      }

      this.$emit("updateTime", this.id, 0);
      this.startButton = require("../assets/play.svg");
    },
    toggleHistory() {
      this.isHistoryShown = !this.isHistoryShown;
    },
  },
  emits: ["remove", "updateState", "updateTime"],
  beforeMount: function () {
    if(this.state === "start") {
      this.interval = setInterval(this.incrementTime, 1000)
      this.startButton = require("../assets/pause.svg");
    }
  },
  beforeUnmount: function () {
    clearInterval(this.interval);
  },
};
</script>

<style scoped>
@import url("../styles/timer.css");
@import url("../styles/history.css");
</style>
