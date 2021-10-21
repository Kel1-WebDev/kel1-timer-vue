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
          <StopwatchItem :name="stopwatches.timer_name" />
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

export default {
  name: "StopwatchList",
  components: {
    StopwatchItem,
  },
  data() {
    return {
      stopwatchName: "",
      stopwatchLists: [],
    };
  },
  methods: {
    addStopwatch() {
      var name = this.stopwatchName;
      var stopwatch = {
        id: this.stopwatchLists.length,
        timer_name: name,
      };

      this.stopwatchLists.push(stopwatch);
    },
  },
};
</script>

<style scoped>
@import url("../styles/form.css");
</style>
