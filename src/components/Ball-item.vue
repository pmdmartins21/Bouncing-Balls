<script lang="ts">
export default {
  name: "Ball-item",
  props: {
    ball: Object,
  },
  mounted() {
    setInterval(this.update, 50);
  },
  data() {
    return {
      maxX: 2500,
      maxY: 1200,
      ballInfo : {
        width: '100px',
        height: '100px',
        backgroundColor: 'black',
        borderRadius: '50px',
        top: `${this.ball.posY}px`,
        left: `${this.ball.posX}px`,
        position: 'absolute',
        transition: '200ms'
      },
      posX: this.ball.posX,
      posY: this.ball.posY,
      direction: this.ball.direction
    };
  },
  methods: {
    update() {
      if (this.posX > this.maxX - 50 || this.posX < 0) {
        this.direction.x = - this.direction.x
      }
      if(this.posY > this.maxY - 25 || this.posY < 100){
          this.direction.y = - this.direction.y
      }

      this.posX += this.direction.x;
      this.ballInfo.left = `${this.posX}px`
      this.posY += this.direction.y;
      this.ballInfo.top = `${this.posY}px`
    },
  },
};

</script>

<template>
  <span :style="ballInfo"></span>
</template>
