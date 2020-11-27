<template>
  <div style="margin-top: 3rem">
    <p style="font-size: 16px; font-weight: bold">Agenda de Reservas</p>
    <div id="visualization">
      <div id="moveLeft" class="buttons-menu" v-on:click="move(0.2)">
        <i class="material-icons dp48">arrow_back</i>
      </div>
      <div id="moveRight" class="buttons-menu" v-on:click="move(-0.2)">
        <i class="material-icons dp48">arrow_forward</i>
      </div>
    </div>
  </div>
</template>
<script>
import vis from "vis";
import moment from "moment";

export default {
  data: function () {
    return {
      timeline: null,
      input: 0,
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
      start: moment().format('YYYY-M-D'),
      zoomMax: 18000000, // 10,000 years is maximum possible
      zoomMin: 10, // 10ms
      showMajorLabels: false,
      timeAxis: { scale: "minute", step: 15 },
      format: {
        minorLabels: function (date) {
          if (date.minutes() == 0) {
            return `<span class="hour">${date.format("h a")}</span>`;
          } else {
            return `<span class="minutes">${date.format("mm")} min</span>`;
          }
        },
      },
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