<template>
  <div>
    <div class="center-content">
      <h1 id="title">cronômetro</h1>
    </div>
    <div class="row">
      <div class="fixed-list">
        <div id="container">
          <stopwatch-item />
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
};
</script>

<style scoped>
@import url("../styles/form.css");
</style>
