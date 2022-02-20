<script lang="ts">
export default {
  name: "App",
  data() {
    return {
      counter: 0,
    }
  },
  methods: {
    clickedBackground() {
      console.log("clicked background");
    },
  },
};
</script>

<template >
  <body @click="clickedBackground">
    <div class="container">
      <div class="box">
      </div>
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
