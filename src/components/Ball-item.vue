<script lang="ts">
export default {
  name: "Ball-item",
  props: {
    ball: Object,
  },
  mounted() {
    //Force the update upon component creation, making the position alter and create movement
    //first argument is the update function that changes the position, 2nd argument is for the update frequency.
    setInterval(this.updateBall, this.ball.time);
  },
  data() {
    return {
      maxX: this.ball.maxX - 25, //max X-Axis translation accounting for ball diameter
      maxY: this.ball.maxY - 25, //max Y-Axis translation accounting for ball diameter
      ballInfo: { //object used for the ball style properties
        width: `${this.ball.size}px`,
        height: `${this.ball.size}px`,
        backgroundColor: `#${Math.floor(Math.random() * 16777215).toString( //create a random color
          16
        )}`,
        borderRadius: `${this.ball.size / 2}px`,
        top: `${this.ball.posY}px`, //initial Y-axis positioning
        left: `${this.ball.posX}px`,//initial X-axis positioning
        position: "absolute",
        transition: `${this.ball.time}ms`,
      },
      xAxis: "x",
      yAxis: "y",
    };
  },
  methods: {
    moveBallX() {
      this.ball.posX += this.ball.velocity.x;
    },
    moveBallY() {
      this.ball.posY += this.ball.velocity.y;
    },
    bounceWall(axis: string) {
      if(axis === this.xAxis) this.ball.velocity.x = -(this.ball.velocity.x * 0.9);
      if(axis === this.yAxis) this.ball.velocity.y = -(this.ball.velocity.y * 0.9);
    },
    checkLimits(axis: string) : boolean {
      if (axis === this.xAxis)
        return this.checkLeftLimit() || this.checkRightLimit();
      if (axis === this.yAxis)
        return this.checkTopLimit() || this.checkBottomLimit();
      return false;
    },
    checkLeftLimit() : boolean {
      return this.ball.posX <= 0;
    },
    checkRightLimit() : boolean {
      return this.ball.posX >= this.maxX - (this.ball.size + 10);
    },
    checkTopLimit() : boolean {
      return this.ball.posY <= 0;
    },
    checkBottomLimit() : boolean {
      return this.ball.posY >= this.maxY - this.ball.size;
    },
    updateBallInfoX() {
      this.ballInfo.left = `${this.ball.posX}px`;
    },
    updateBallInfoY() {
      this.ballInfo.top = `${this.ball.posY}px`;
    },
    adjustVelocityY() {
      this.ball.velocity.y += this.ball.gravity;
    },
    //altering the ball positioning
    updateBall() {
      //inverting direction after horizontal/vertical wall hit and adjusting speed by 0.9.
      if (this.checkLimits(this.xAxis)) this.bounceWall(this.xAxis);
      if (this.checkLimits(this.yAxis)) this.bounceWall(this.yAxis);
      //X-axis Motion
      //move ball X-axis position by its velocityX vector
      this.moveBallX();

      //limit x translate into window width, adjusting value if it goes over the limit
      this.checkRightLimit()
        ? (this.ball.posX = this.maxX - (this.ball.size + 10))
        : this.ball.posX;
      this.checkLeftLimit() ? (this.ball.posX = -5) : this.ball.posX;

      //reflecting the movement on the object itself
      this.updateBallInfoX();

      //Y-axis Motion
      //adjusting velocityY vector for gravity (v = vo -gt)
      //Since t is included in the update() method we only include gravity
      this.adjustVelocityY();

      //move ball Y-axis position by its velocityY vector
      this.moveBallY();

      //limit y translate into window height, adjusting value if it goes over the limit
      this.checkBottomLimit()
        ? (this.ball.posY = this.maxY - this.ball.size)
        : this.ball.posY;
      this.checkTopLimit() ? (this.ball.posY = 0) : this.ball.posY;

      //reflecting the movement on the object itself
      this.updateBallInfoY();
    },
  },
};
</script>

<template>
  <span :style="ballInfo"></span>
</template>
