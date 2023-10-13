<template>
  <header>Barcode-Scanner</header>
  <button @click="toggleText">Scan</button>
  <p v-if="successTest">  Gescannt</p>
  <StreamBarcodeReader
    @decode="onDecode"
    @loaded="onLoaded"
  ></StreamBarcodeReader>
</template>

<script>
import { StreamBarcodeReader } from "vue-barcode-reader";
export default {
  data() {
    return {
      successTest: false
    };
  },
  methods: {
    onDecode(text) {
      console.log(`Decode text from QR code is ${text}`)
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