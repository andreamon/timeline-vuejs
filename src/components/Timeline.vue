<template>
  <div id="visualization">
    <!-- <div class="menu">
    </div> -->
    <div id="moveLeft" class="buttons-menu" v-on:click="move(0.2)">
        <i class="material-icons dp48">arrow_back</i>
    </div>
    <div id="moveRight" class="buttons-menu" v-on:click="move(-0.2)">
      <i class="material-icons dp48">arrow_forward</i>
    </div>
  </div>
</template>
<script>
import vis from "vis";
export default {
  data: function () {
    return {
      timeline: null,
    };
  },
  name: "Timeline",
  props: ["reservas"],
  watch: {
    reservas: function () {
      this.timeline.setItems(this.reservas);
    },
  },
  mounted: function () {
    console.log(this.reservas);
    // create a timeline with some data
    var container = document.getElementById("visualization");
    var options = {
      orientation: {
        axis: "top",
        item: "top",
      },
      zoomMax: 87600900, // 10,000 years is maximum possible
      zoomMin: 10000000, // 10ms
    };
    this.timeline = new vis.Timeline(container, this.reservas, options);
  },
  methods: {
    move: function (percentage) {
      var range = this.timeline.getWindow();
      var interval = range.end - range.start;
      this.timeline.setWindow({
        start: range.start.valueOf() - interval * percentage,
        end: range.end.valueOf() - interval * percentage,
      });
    },
  },
};
</script>
<style>
@import "../assets/styles/timeline.css";
</style>