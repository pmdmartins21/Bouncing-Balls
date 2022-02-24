<script lang="ts">
import BallsItems from "./components/Balls-items.vue";

export default {
  name: "App",
  components: { BallsItems },
  data() {
    return {
      counter: 0,
      balls: [],
    };
  },
  methods: {
    //instantiate and launch a ball passing the coordinates as props.
    clickedBackground(event: MouseEvent) {
      console.log("clicked background");
      //get the coordinates and save them in the variables
      let mouseX = event.pageX;
      let mouseY = event.pageY;
      let radius = 5;

      let newBall = {
        id: this.counter,
        posX: mouseX,
        posY: mouseY,
        size: radius,
        direction: {
          x: -100 + Math.floor(Math.random() * 200),
          y: -100 + Math.floor(Math.random() * 200),
        }
      };

      this.balls = [... this.balls, newBall];
      this.counter++;
    },
  },
};
</script>

<template >
  <body @click="clickedBackground">
    <div class="container">
      <BallsItems :balls="balls" />
      <canvas class="box" style="top:0px; left:0px"></canvas>
    </div>
  </body>
  
</template>

<style>
.box {
  width: 1200px;
  height: 600px;
  display: flex;
  border: 10px #333 solid;
  position: absolute;
}
</style>
