<script lang="ts">
import BallItem from "./Ball-item.vue";

export default {
  name: "Balls-items",
  props: {
    balls: Array,
  },
  components: { BallItem },
};
</script>

<template>
  <div :key="balls.id" v-for="ball in balls">
    <BallItem :ball="ball" />
  </div>
</template>
