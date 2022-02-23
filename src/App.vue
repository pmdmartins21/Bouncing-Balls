

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
      <p>Coordenadas</p>
      <p>X: {{ mouseX }}</p>
      <p>Y: {{ mouseY }}</p>
      <div class="box"></div>
    </div>
  </body>
  
</template>

<style>
.box {
  width: 800px;
  height: 800px;
  display: flex;
  border: 5px #333 solid;
  margin: auto;
}
</style>
