<template>
  <div>
    <div class="container">
      <h1 name class="name dark-blue">{{name}}</h1>
      <img delete class="del-btn" src="../assets/delete.svg" />
    </div>
    <div>
      <div class="blabla">
        <!-- CONVERTNYA BISA CALL FUNCTION DI SINI, DENGAN PARAMETER time -->
        <!-- CONTOH: convertTimer(time) -->
        <p time class="time">{{time}}</p>
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
  </div>
</template>

<script>
export default {
  name: "StopwatchItem",
  props:{
    name:{
      type:String,
      required:true
    },
    // timer MASIH BERBENTUK NUMBER
    // HARUS DICONVERT KE FORMAT 00:00:00 TERLEBIH DAHULU
    time:{
      type:Number,
      required:true
    }
  }
};
</script>

<style scoped>
@import url("../styles/timer.css");
@import url("../styles/history.css");
</style>
