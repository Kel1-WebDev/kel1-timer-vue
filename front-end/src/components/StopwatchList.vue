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
  beforeMount() {
    this.loadStopwatch();
  },
  methods: {
    addStopwatch() {
      var name = this.stopwatchName;
      var stopwatch = {
        id: this.lastId,
        timer_name: name,
        time: 0,
        state: "stop",
      };

      this.stopwatchLists.push(stopwatch);
      this.lastId++;
      this.stopwatchName = "";

      if (this.stopwatchLists.length >= 10) {
        this.disableCreateButton();
      }
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
      this.enableCreateButton();
      this.stopwatchLists.splice(this.searchTimer(id), 1);
    },
    loadStopwatch() {
      axios.get("http://localhost:3000/timer").then(
        function(stopwatches) {
          if (stopwatches.data.length > 0) {
            this.lastId = stopwatches.data[stopwatches.data.length - 1].id + 1;
          } else {
            this.lastId = 0;
          }

          this.stopwatchLists = stopwatches.data;

          if (this.stopwatchLists.length >= 10) {
            this.disableCreateButton();
          }
        }.bind(this)
      );
    },
    enableCreateButton() {
      document.getElementById("submit").disabled = false;
      document.getElementById("submit").style["background"] = "#191BA9";
      document.getElementById("submit").style["border"] = "#191BA9";
    },
    disableCreateButton() {
      document.getElementById("submit").disabled = true;
      document.getElementById("submit").style["background"] = "#CCCCCC";
      document.getElementById("submit").style["border"] = "transparent";
    },
  },
};
</script>

<style scoped>
@import url("../styles/form.css");
</style>
