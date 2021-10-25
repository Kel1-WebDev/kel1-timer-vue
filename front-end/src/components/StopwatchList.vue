<template>
  <div style="display: flex; flex-direction: column">
    <div class="center-content">
      <h1 id="title">cronômetro</h1>
    </div>
    <div class="row">
      <div class="fixed-list">
        <div id="container">
          <StopwatchItem
            :key="stopwatches.id"
            :id="stopwatches.id"
            :name="stopwatches.timer_name"
            :time="stopwatches.time"
            :state="stopwatches.state"
            v-for="stopwatches in stopwatchLists"
            @updateTime="updateTime"
            @updateState="updateState"
            @remove="removeTimer"
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
            <input
              id="submit"
              type="button"
              value="Create Stopwatch"
              @click="addStopwatch"
            />
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import StopwatchItem from "./StopwatchItem.vue";
import axios from "axios";

export default {
  name: "StopwatchList",
  components: {
    StopwatchItem,
  },
  data() {
    return {
      stopwatchName: "",
      stopwatchLists: [],
      lastId: 0,
    };
  },
  methods: {
    addStopwatch() {
      var name = this.stopwatchName;
      axios.post('http://localhost:3000/timer', { timer_name: name })
        .then((response) => {
          console.log(response);
          var stopwatch = {
            id: response.data.id,
            timer_name: name,
            time: 0,
            state: "stop",
          };
          this.stopwatchLists.push(stopwatch);
        })
        .error((err) => {
          console.error(err);
        })
    },
    searchTimer(id) {
      for (let i = 0; i < this.stopwatchLists.length; i++) {
        if (this.stopwatchLists[i].id == id) {
          return i;
        }
      }

      return -1;
    },
    updateTime(id, time) {
      this.stopwatchLists[this.searchTimer(id)].time = time;
    },
    updateState(id, state) {
      this.stopwatchLists[this.searchTimer(id)].state = state;
    },
    removeTimer(id) {
      this.stopwatchLists.splice(this.searchTimer(id), 1);
    },
  },
};
</script>

<style scoped>
@import url("../styles/form.css");
</style>
