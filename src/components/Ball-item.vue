<script lang="ts">
export default {
  name: "Ball-item",
  props: {
    ball: Object,
  },
  mounted() {
    setInterval(this.update, 100 );
  },
  data() {
    return {
      maxX: 1220,
      maxY: 620,
      ballInfo : {
        width: '100px',
        height: '100px',
        backgroundColor: 'black',
        borderRadius: '50px',
        top: `${this.ball.posY}px`,
        left: `${this.ball.posX}px`,
        position: 'absolute',
        transition: '100ms'
      },
      posX: this.ball.posX,
      posY: this.ball.posY,
      direction: this.ball.direction
    };
  },
  methods: {
    //altering the ball positioning
    update() {
      //inverting direction after horizontal/vertical wall hit and adjusting speed by 0.9.
      if (this.posX >= this.maxX - 110 || this.posX <= 10) {
        this.direction.x = - (this.direction.x * 0.9);
      }
      if (this.posY >= this.maxY - 110 || this.posY <= 10) {
        this.direction.y = - (this.direction.y * 0.9);
      }

      this.posX +=this.direction.x;
      //limit x translate into canvas width
      this.posX > this.maxX - 110 ? (this.posX = this.maxX - 110) : this.posX;
      this.posX < 10 ? (this.posX = 10) : this.posX;
      this.ballInfo.left = `${this.posX}px`

      this.direction.y+= 5
      this.posY += this.direction.y;
      //limit y translate into canvas height
      this.posY > this.maxY - 110 ? (this.posY = this.maxY - 110) : this.posY;
      this.posY < 10 ? (this.posY = 10) : this.posY;
      this.ballInfo.top = `${this.posY}px`
    },
  },
};

</script>

<template>
  <span :style="ballInfo"></span>
</template>
