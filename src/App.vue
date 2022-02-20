<script lang="ts">
export default {
  name: "App",
  data() {
    return {
      MouseX: null,
      MouseY: null,
    }
  },
  methods: {
    //function to instantiate and launch a ball passing the coordinates as props.
    clickedBackground(event: MouseEvent) {
      console.log("clicked background");
      //get the coordinates and save them in the variables
      this.MouseX = event.pageX;
      this.MouseY = event.pageY;
    },
  },
};
</script>

<template >
  <body @click="clickedBackground ">
    <div class="container">
      <p>Coordenadas</p>
      <p>X: {{ MouseX }}</p>
      <p>Y: {{ MouseY }}</p>
      <div class="box"></div>
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
