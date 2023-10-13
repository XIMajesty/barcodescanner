<template>
  <header>Barcode-Scanner</header>
  <button @click="toggleKamera">Start Scan</button>
  <p v-if="successTest">  Gescannt</p>
  <StreamBarcodeReader
    @decode="onDecode"
    @loaded="onLoaded"
    v-if="successTest"
  ></StreamBarcodeReader>
  <p>{{ decodedText }}</p>
  <img src="https://img.offers-cdn.net/assets/uploads/offers/de/20595789/limetto-cola-mix-o-cola-mix-zero-20-500-ml-large.jpeg" alt="Cola-Mix Limonade" v-if="decodedText == 42261322">
</template>

<script>
import { StreamBarcodeReader } from "vue-barcode-reader";
export default {
  data() {
    return {
      decodedText: null,
      successTest: false,
    };
  },
  components: {
    StreamBarcodeReader,
  },
  methods: {
    onDecode(text) {
      console.log(`Decode text from QR code is ${text}`)
      this.decodedText = text
      this.successTest = !this.successTest;

    },
    onLoaded() {
      console.log(`Ready to start scanning barcodes`)
    },
    toggleKamera() {
      this.successTest = !this.successTest;
    }
  }
};
</script>