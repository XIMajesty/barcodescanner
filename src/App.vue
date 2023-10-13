<template>
  <div>
    <button @click="startScanning">Start Scan</button>
    <p v-if="decodedText">Decoded text: {{ decodedText }}</p>
    <stream-barcode-reader v-if="scannerEnabled" @newCode="onDecode"></stream-barcode-reader>
  </div>
</template>

<script>
import { StreamBarcodeReader } from "vue-barcode-reader";

export default {
  data() {
    return {
      decodedText: null,
      scannerEnabled: false,
    };
  },
  components: {
    StreamBarcodeReader,
  },
  methods: {
    onDecode(code) {
      this.decodedText = code;
    },
    startScanning() {
      this.scannerEnabled = !this.scannerEnabled;
    },
  },
};
</script>