<template>
  <div class="container">
    <h1 name class="name dark-blue">WebDev Teori</h1>
    <img delete class="del-btn" src="../assets/delete.svg" />
  </div>
  <div>
    <div class="blabla">
      <p time class="time">00:00:00</p>
      <div class="container">
        <img start class="timer-btn" src="../assets/play.svg" />
        <img stop class="timer-btn dark-blue" src="../assets/stop.svg" />
      </div>
    </div>
  </div>
  <div>
    <div history class="history">
      <button showHistory class="accordion"><span> ▶ </span> History</button>
      <div historyList class="history-list"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "StopwatchItem",
};
</script>

<style scoped>
@import url("../styles/timer.css");
@import url("../styles/history.css");
</style>
