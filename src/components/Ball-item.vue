<script lang="ts">
export default {
  name: "Ball-item",
  props: {
    ball: Object,
  },
  data() {
    return {
      ballInfo : {
        width: '4rem',
        height: '4rem',
        backgroundColor: 'black',
        borderRadius: '2rem',
        top: `${this.ball.posY - 30}px`,
        left: `${this.ball.posX -30}px`,
        position: 'absolute'
      },
    };
  },
};

</script>

<template>
  <span :style="ballInfo"></span>
</template>