<script lang="ts">
export default {
  name: "Ball-item",
  props: {
    ball: Object,
  },
  mounted() {
    //Force the update upon component creation, making the position alter and create movement
    //first argument is the update function that changes the position, 2nd argument is for the update frequency.
    setInterval(this.update, this.ball.time);
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
    };
  },
  methods: {
    //altering the ball positioning
    update() {
      //inverting direction after horizontal/vertical wall hit and adjusting speed by 0.9.
      if (this.ball.posX >= this.maxX - ( this.ball.size + 10) || this.ball.posX <= 0) {
        this.ball.velocity.x = -(this.ball.velocity.x * 0.9);
      }
      if (this.ball.posY >= this.maxY - ( this.ball.size) || this.ball.posY <= 0) {
        this.ball.velocity.y = -(this.ball.velocity.y * 0.9);
      }

      //X-axis Motion
      //move ball X-axis position by its velocityX vector
      this.ball.posX += this.ball.velocity.x;

      //limit x translate into window width, adjusting value if it goes over the limit
      this.ball.posX > this.maxX - (this.ball.size + 10)
        ? (this.ball.posX = this.maxX - (this.ball.size + 10))
        : this.ball.posX;
      this.ball.posX < 0 ? (this.ball.posX = -10) : this.ball.posX;
      
      //reflecting the movement on the object itself
      this.ballInfo.left = `${this.ball.posX}px`;

      //Y-axis Motion
      //adjusting velocityY vector for gravity (v = vo -gt)
      //Since t is included in the update() method we only include gravity
      this.ball.velocity.y += this.ball.gravity;
      
      //move ball Y-axis position by its velocityY vector
      this.ball.posY += this.ball.velocity.y;
      
      //limit y translate into window height, adjusting value if it goes over the limit
      this.ball.posY > this.maxY - this.ball.size
        ? (this.ball.posY = this.maxY - this.ball.size)
        : this.ball.posY;
      this.ball.posY < 0 ? (this.ball.posY = 0) : this.ball.posY;
      
      //reflecting the movement on the object itself
      this.ballInfo.top = `${this.ball.posY}px`;
    },
  },
};
</script>

<template>
  <span :style="ballInfo"></span>
</template>
