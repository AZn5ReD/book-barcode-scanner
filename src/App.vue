<template>
  <div id="app">
    <button @click="showNewCode('9783940862211')">test</button>
    <Camera @newCode="showNewCode($event)" />
    <Popup :popup="popup" :code="code" :book="book" />
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
      code: "",
      popup: false
    };
  },
  methods: {
    async showNewCode(code) {
      if (this.controlCode(code)) {
        this.book = await this.getBookInfo(code);
        this.code = code;
        this.popup = true;
      }
    },
    controlCode(code) {
      if (code.length === 9 || code.length === 10 || code.length === 13)
        return true;
      else return false;
    },
    async getBookInfo(code) {
      const url = "https://www.googleapis.com/books/v1/volumes?q=isbn:" + code;

      try {
        const response = await fetch(url);
        const results = await response.json();
        return results.items[0];
      } catch {
        return null;
      }
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
