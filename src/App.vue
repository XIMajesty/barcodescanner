<template>
<<<<<<< HEAD
  <header>Barcode-Scanner</header>
  <button @click="toggleKamera">Scan</button>
  <p v-if="successTest">  Gescannt</p>
=======
  <body>
    <header>Barcode-Scanner</header>
  <button @click="toggleText">Scan</button>
  <p v-if="successTest">Gescannt</p>
>>>>>>> d4454e582626d9c4b222d20ce25e00e7921c1496
  <StreamBarcodeReader
    @decode="onDecode"                                              
    @loaded="onLoaded"
    v-if="successTest"
  ></StreamBarcodeReader>
  <p>{{ decodedText }}</p>
<<<<<<< HEAD
=======
  </body>
>>>>>>> d4454e582626d9c4b222d20ce25e00e7921c1496
</template>

<script>
import { StreamBarcodeReader } from "vue-barcode-reader";
export default {
  data() {
    return {
      decodedText: null,
<<<<<<< HEAD
      successTest: false,
=======
      successTest: false
>>>>>>> d4454e582626d9c4b222d20ce25e00e7921c1496
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
    toggleKamera() {
      this.successTest = !this.successTest;
    }
  }
};
</script>

<style>
</style>