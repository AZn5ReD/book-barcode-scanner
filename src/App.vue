<template>
  <div id="app">
    <Camera @newCode="showNewCode($event)" />
    <Popup v-if="showPopup" :code="code" :book="book" />
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
    async showNewCode(code) {
      if (this.controlCode(code)) {
        const title = await this.getBookInfo(code);
        this.code = code;
        this.showPopup = true;
      }
    },
    controlCode(code) {
      if (code.length === 10 || code.length === 13) return true;
      else return false;
    },
    async getBookInfo(code) {
      const url = "https://www.googleapis.com/books/v1/volumes?q=isbn:" + code;

      const response = await fetch(url);
      const results = await response.json();

      if (results.totalItems) {
        this.book = results.items[0];
      }
      return this.book ? true : false;
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
