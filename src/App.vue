<template>
  <div id="app">
    <Camera @newCode="showNewCode($event)" />
    <Popup v-if="showPopup" :code="code" />
  </div>
</template>

<script>
import Camera from "./components/Camera";
import Popup from "./components/Popup";

export default {
  name: "app",
  components: {
    Camera,
    Popup
  },
  data() {
    return {
      books: [],
      book: {},
      showPopup: false,
      code: ""
    };
  },
  methods: {
    showNewCode(code) {
      this.code = code;
      this.showPopup = true;
    }
  }
};
</script>

<style>
html,
body {
  width: 100%;
  background-color: black;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: black;
  width: 100%;
}
</style>
