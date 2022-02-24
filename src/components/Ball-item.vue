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
      ballInfo : {
        width: '4rem',
        height: '4rem',
        backgroundColor: 'black',
        borderRadius: '2rem',
        top: `${this.ball.posY - 20}px`,
        left: `${this.ball.posX - 30}px`,
        position: 'absolute'
      },
      posX: this.ball.posX,
      posY: this.ball.posY,
    };
  },
  methods: {
    shout() {
      console.log("teste")
    },
    update() {
      this.posX += 20;
      this.ballInfo.left = `${this.posX - 30}px`
    },
  },
};

</script>

<template>
  <span :style="ballInfo"></span>
</template>
