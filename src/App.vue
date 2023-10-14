<template>
  <header>
    <p id="header">Barcode-Scanner</p>
  </header>
  <body>
    <button @click="toggleKamera">Start Scan</button>
    <p v-if="successTest"> Scanning</p>
    <StreamBarcodeReader @decode="onDecode" @loaded="onLoaded" v-if="successTest"></StreamBarcodeReader>
    <p>{{ decodedText }}</p>
    <img src="https://img.offers-cdn.net/assets/uploads/offers/de/20595789/limetto-cola-mix-o-cola-mix-zero-20-500-ml-large.jpeg" alt="Cola-Mix Limonade" v-if="decodedText == 42261322">
  </body>
</template>

<script>
import { StreamBarcodeReader } from "vue-barcode-reader";
import axios from "axios"; // Import Axios

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
      console.log(`Decoded text from QR code is ${text}`);
      this.decodedText = text;
      this.successTest = !this.successTest;

      // Send the decoded barcode to the server using Axios
      this.sendBarcodeToServer(text);
    },
    onLoaded() {
      console.log(`Ready to start scanning barcodes`);
    },
    toggleKamera() {
      this.successTest = !this.successTest;
    },
    async sendBarcodeToServer(barcode) {
      try {
        const response = await axios.post("http://localhost:8080/barcodes", {
          barcode: barcode,
        });

        console.log("Barcode saved:", response.data);
      } catch (error) {
        console.error("There was an error!", error);
      }
    },
  },
};
</script>

<style>
/* Global styles */
body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
  background-color: #212020;
}

#header {
  background-color: #333;
  color: #fff;
  text-align: center;
  padding: 10px 0;
  font-size: 24px;
  margin-bottom: 20px;
  border-radius: 5px;
}

button {
  display: block;
  background-color: #007BFF;
  color: #fff;
  text-align: center;
  border: none;
  border-radius: 5px;
  padding: 15px;
  width: 100%;
  cursor: pointer;
  font-size: 18px;
  margin-bottom: 20px;
}

button:active {
  background-color: #0056b4;
}

p {
  color: white;
  text-align: center;
  padding: 10px;
  border-radius: 5px;
  font-size: 16px;
}

img {
  max-width: 100%;
  /* Makes sure the image doesn't overflow its parent container */
  display: block;
  margin: 15px auto;
  border-radius: 5px;
}

/* Responsive design adjustments */

/* For tablets or smaller screens */
@media (max-width: 768px) {
  header {
    font-size: 20px;
  }

  button {
    padding: 12px;
    font-size: 16px;
  }
}

/* For smartphones or very small screens */
@media (max-width: 480px) {
  header {
    font-size: 18px;
  }

  button {
    padding: 10px;
    font-size: 14px;
  }

  p {
    font-size: 14px;
  }
}
</style>
