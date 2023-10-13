<template>
  <header>
    <h1 class="center">Barcode-Scanner</h1>
  </header>
  <body id="body">
    <section id="firstSection">
      <button @click="toggleKamera" class="center">Start Scan</button>
    <p v-if="successTest" class="center">Gescannt</p>
    <StreamBarcodeReader @decode="onDecode" @loaded="onLoaded" v-if="successTest"></StreamBarcodeReader>
    <p class="center">{{ decodedText }}</p>
    <img src="https://img.offers-cdn.net/assets/uploads/offers/de/20595789/limetto-cola-mix-o-cola-mix-zero-20-500-ml-large.jpeg" alt="Cola-Mix Limonade" v-if="decodedText == 42261322">
    </section>
    <section id="secondSection">

    </section>
  </body>
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

<style>
  #body{
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 80%;
  }

  .center{
    display:flex;
    justify-content: center;
    align-items: center;
    margin-left: auto;
    margin-right: auto;
  }
</style>