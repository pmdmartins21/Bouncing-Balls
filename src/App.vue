<script lang="ts">
import BallsItems from "./components/Balls-items.vue";

const GRAVITY = 9.81; //Value for the gravity force acceleration
const MinBallSize = 50; //Mandatory
const MaxBallSize = 100; //Mandatory
const TIME = 100 //Variable to be used in the update method for Ball component. Lower values mean higher refresh rate.

export default {
  name: "App",
  components: { BallsItems },
  data() {
    return {
      counter: 0,
      balls: [],
      innerWidth: 0,
      innerHeight: 0,
    };
  },
  mounted() {
    //get full screen size
    this.innerWidth = window.innerWidth;
    this.innerHeight = window.innerHeight;
  },
  methods: {
    //instantiate and launch a ball passing the coordinates as props upon clicking.
    clickedBackground(event: MouseEvent) {
      //get the coordinates for the click event and save them in the variables
      let mouseClickX = event.pageX;
      let mouseClickY = event.pageY;

      //base for instantiating new balls and adding to ball array
      let newBall = {
        id: this.counter,
        posX: mouseClickX,
        posY: mouseClickY,
        size: Math.floor(
          //generate a random sized ball between 50-100px
          Math.random() * (MaxBallSize - MinBallSize) + MinBallSize
        ),
        //initial velocity vector that includes vx and vy for direction and speed
        velocity: {
          x: -100 + Math.floor(Math.random() * 200),
          y: -100 + Math.floor(Math.random() * 200),
        },
        maxX: innerWidth, //passing the maximum X-axis transalation possible
        maxY: innerHeight, //passing the maximum Y-axis transalation possible
        time: TIME,
        gravity: GRAVITY,
      };
      //adding the new ball to the balls array
      this.balls = [...this.balls, newBall];
      //increasing counter for next id used in key binding
      this.counter++;
    },
  },
};
</script>

<template>
  <body >
    <div class="container" @click="clickedBackground">
      <BallsItems :balls="balls" />
    </div>
  </body>
</template>

<style>
.container {
  height:95%;
  width: 95%;
  position: absolute;
}
</style>
