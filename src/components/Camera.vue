<template>
  <div class="video_container">
    <div class="video" />
  </div>
</template>

<script>
import Quagga from "quagga";

export default {
  name: "Camera",
  data() {
    return {
      lastCode: ""
    };
  },
  mounted() {
    Quagga.init(
      {
        inputStream: {
          name: "Live",
          type: "LiveStream",
          target: document.querySelector(".video"),
          constraints: {
            facingMode: "environment"
          }
        },
        decoder: {
          readers: ["ean_reader", "ean_8_reader"]
        }
      },
      function(err) {
        if (err) {
          console.error(err);
          return;
        }
        console.info("Quagga initialization finished.");
        Quagga.start();
      }
    );
    Quagga.onDetected(
      function(result) {
        let code = result.codeResult.code;

        if (this.lastCode !== code) {
          this.lastCode = code;
          this.$emit("newCode", code);
        }
      }.bind(this)
    );
    // document.querySelector("video").requestFullscreen();
  },
  destroyed() {
    Quagga.stop();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.camera {
  width: 100%;
}

video {
  max-width: 100%;
  width: 100%;
}
.video_container {
  position: relative;
  height: 50vh;
  width: 100%;
}

.video {
  height: 100%;
  width: 100%;
  overflow: hidden;
}

.video video {
  width: 100%;
}
</style>
