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
          <img start class="timer-btn" src="../assets/play.svg" @click="start()"/>
          <img stop class="timer-btn dark-blue" src="../assets/stop.svg" @click="stop()"/>
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
          <li v-for="(item,index) in histories" :key="index"> 
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
  data: function () {
    return {
      time: 0,
      state: "stop",
      interval: null,
      histories: [],
      isHistoryShown: false
    }
  },
  methods: {
    insertZero(time) {
      if (time < 10)
        return "0" + time;
      return time;
    },
    formatTime(second) {
      let divisor = 60 * 60;

      const hour = Math.floor(second / divisor);
      second = second % divisor;
      divisor = divisor / 60;

      const minute = Math.floor(second / divisor);
      second = second % divisor;

      return this.insertZero(hour) + ":" + this.insertZero(minute) + ":" + this.insertZero(second);
    },
    incrementTime() {
      this.time++;
    },
    start() {
      if ((this.state === "pause") || (this.state === "stop")) {
        this.state = "start";
        this.interval = setInterval(this.incrementTime, 1000);
      }
      else if (this.state === "start"){
        this.state = "pause";
        clearInterval(this.interval);
      }
    },
    stop() {
      this.state = "stop";
      clearInterval(this.interval);
      
      if (this.time > 0) {
        this.histories.push(this.time);
      }

      this.time = 0;
    },
    toggleHistory() {
      this.isHistoryShown = !this.isHistoryShown;
    }
  },
};
</script>

<style scoped>
@import url("../styles/timer.css");
@import url("../styles/history.css");
</style>
