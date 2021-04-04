<template>
  <div id="app">
    <input type="file" @change="imageInputed" />
    <img :src="inputedImageSrc" />
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import EXIF from "exif-js";
export default {
  name: "App",
  components: {
    HelloWorld,
  },
  data() {
    return {
      inputedFile: {},
      inputedImageSrc: "",
    };
  },
  methods: {
    imageInputed(event) {
      this.inputedFile = event.target.files[0];
      const reader = new FileReader();
      reader.readAsDataURL(this.inputedFile);
      reader.onload = () => {
        this.inputedImageSrc = reader.result;
      };
      EXIF.getData(this.inputedFile, function () {
        console.debug("debug2 :", this);
        console.debug(EXIF.getAllTags(this));
      });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
