<template>
  <div class="camera"></div>
</template>

<script>
import Quagga from "quagga";

export default {
  name: "Camera",
  mounted() {
    Quagga.init(
      {
        inputStream: {
          name: "Live",
          type: "LiveStream",
          target: document.querySelector(".camera"),
          constraints: {
            width: "100%",
            facingMode: "environment"
          }
        },
        decoder: {
          readers: ["code_128_reader", "ean_reader", "ean_8_reader"]
        }
      },
      function(err) {
        if (err) {
          console.log(err);
          return;
        }
        console.log("Initialization finished. Ready to start");
        Quagga.start();
      }
    );
    Quagga.onDetected(function(result) {
      var code = result.codeResult.code;

      // if (App.lastResult !== code) {
      //   App.lastResult = code;
      alert(code);
      // }
    });
  },
  destroyed() {
    Quagga.stop();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.camera {
  height: 100%;
}
</style>
