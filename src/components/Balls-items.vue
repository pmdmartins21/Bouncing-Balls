<template>
  <BallItem />
  <p>Balls balls</p>
</template>

<script lang="ts">
import BallItem from "./Ball-item.vue";
export default {
  name: "Balls-items",
  props: {
    balls: Array,
  },
  components: { BallItem }
} 
</script>