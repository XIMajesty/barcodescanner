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
  <img src="https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.prospektangebote.de%2Fgeschaefte%2Fnetto-getraenke-discount%2Fangebote%2Flimetto-cola-mix-o-cola-mix-zero-20-500-ml-angebot-20595789%2F&psig=AOvVaw00tjwK0Q0lAh_MJiVuOXjP&ust=1697296085067000&source=images&cd=vfe&opi=89978449&ved=0CA8QjRxqFwoTCIjt7uqm84EDFQAAAAAdAAAAABAD" alt="Cola-Mix Limonade" v-if="decodedText == 42261322">
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