<template>
  <body>
    <header>Barcode-Scanner</header>
  <button @click="toggleText">Scan</button>
  <p v-if="successTest">Gescannt</p>
  <StreamBarcodeReader
    @decode="onDecode"                                              
    @loaded="onLoaded"
    v-if="successTest"
  ></StreamBarcodeReader>
  <p>{{ decodedText }}</p>
  </body>
</template>

<script>
import { StreamBarcodeReader } from "vue-barcode-reader";
export default {
  data() {
    return {
      decodedText: null,
      successTest: false
    };
  },
  components: {
    StreamBarcodeReader,
  },
  methods: {
    onDecode(text) {
      console.log(`Decode text from QR code is ${text}`)
      decodedText = text
    },
    onLoaded() {
      console.log(`Ready to start scanning barcodes`)
    },
    toggleText() {
      this.successTest = !this.successTest;
    }
  }
};
</script>

<style>
</style>