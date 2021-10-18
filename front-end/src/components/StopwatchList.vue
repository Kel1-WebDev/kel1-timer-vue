<template>
  <div style="display: flex; flex-direction: column">
    <div class="center-content">
      <h1 id="title">cronômetro</h1>
    </div>
    <div class="row">
      <div class="fixed-list">
        <div
          v-for="stopwatches in stopwatchLists"
          :key="stopwatches.id"
          id="container"
        >
          <StopwatchItem 
          :name="stopwatches.timer_name" 
          :time="stopwatches.time"
          />
        </div>
      </div>
      <div>
        <div id="form">
          <form>
            <h2>CREATE NEW STOPWATCH</h2>
            <label for="stopwatch-name">Insert a new stopwatch's label</label>
            <input
              type="text"
              id="stopwatch-name"
              name="stopwatch-name"
              placeholder="Enter the label"
              v-model="stopwatchName"
              @keyup.enter="addStopwatch"
            />
            <input id="submit" type="button" value="Create Stopwatch" />
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import StopwatchItem from "./StopwatchItem.vue";

export default {
  name: "StopwatchList",
  components: {
    StopwatchItem,
  },
  data() {
    return {
      stopwatchName: "",
      stopwatchLists: [
        {
          id: 10,
          timer_name: "Webdev",
          time: 59,
          state: "pause",
        },
        {
          id: 11,
          timer_name: "Komnum",
          time: 87,
          state: "start",
        },
      ],
    };
  },
  methods: {
    addStopwatch() {
      // TULIS CODE UNTUK PUSH ARRAY OF OBJECT stopwatchLists
      // ALERT HANYA UNTUK TESTING APAKAH INPUT stopwatchName BERHASIL DIKIRIM
      alert(this.stopwatchName);
    },
  },
};
</script>

<style scoped>
@import url("../styles/form.css");
</style>
