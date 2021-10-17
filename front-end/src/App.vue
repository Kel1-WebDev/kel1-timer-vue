<template>
  <div id="main" class="center-content background-illustration background-broken-white">
    <stopwatch-list />
  </div>
</template>

<script>
import StopwatchList from "./components/StopwatchList.vue";

export default {
  name: "App",
  components: {
    StopwatchList,
  },
};
</script>

<style>
@import url("./styles/main.css");
</style>
