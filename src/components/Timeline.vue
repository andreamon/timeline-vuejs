<template>
  <div id="visualization">
    <div class="menu">
      <input
        style="display: none"
        id="sliderZoom"
        type="range"
        class="range"
        name="a"
        min="-1"
        max="1"
        step="0.1"
        value="0"
      />
      <i class="material-icons dp48 buttons-menu" id="fit">home</i>
      <i class="material-icons dp48 buttons-menu" id="moveLeft">arrow_back</i>
      <i class="material-icons dp48 buttons-menu" id="moveRight"
        >arrow_forward</i
      >
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
    // var items = new vis.DataSet([
    //   {
    //     id: 1,
    //     content: "Reserva 1",
    //     start: "2019-03-1 10:00",
    //     end: "2019-03-1 10:30",
    //   },
    //   {
    //     id: 2,
    //     content: "Reserva 2",
    //     start: "2019-03-1 11:00",
    //     end: "2019-03-1 11:45",
    //   },
    // ]);
    var options = {
      //stack: false,
      orientation: {
        axis: "top",
        item: "top",
      },
      //zoomMax: 31536000000, // just one year
      zoomMax: 87600900, // 10,000 years is maximum possible
      zoomMin: 10000000, // 10ms
    };
    // new vis.Timeline(container, items, options);
    this.timeline = new vis.Timeline(container, this.reservas, options);
  },
};
</script>
<style>
@import "../assets/styles/timeline.css";
</style>