<template>
  <header>
    <p id="header">Barcode-Scanner</p>
  </header>

  <body>
    <button id="scanButton" @click="toggleKamera" v-if="successTest == false">Start Scan</button>
    <button id="scanButton" @click="toggleKamera" v-if="successTest == true">Stop Scan</button>
    <p v-if="successTest"> Scanning</p>
    <StreamBarcodeReader @decode="onDecode" @loaded="onLoaded" v-if="successTest"></StreamBarcodeReader>
    <p>{{ decodedText }}</p>
    <img src="https://img.offers-cdn.net/assets/uploads/offers/de/20595789/limetto-cola-mix-o-cola-mix-zero-20-500-ml-large.jpeg" alt="Cola-Mix Limonade" v-if="decodedText == 42261322 && successTest == false">
    <img src="https://expressdrinks.de/media/image/54/61/50/10010308_0_8.png" alt="Wasser" v-if="decodedText == 4005906003724 && successTest == false">
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
      test: 42261322,
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
      this.decodedText = barcode
      this.test++
      try {
        const response = await axios.post("http://localhost:3000/barcodes", {
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
  font-size: 24px;
  border: 1px rgb(0, 0, 0);

  text-align: center;
  padding: 5px;
  margin-bottom: 20px;
  margin-left: 70px;
  margin-right: 70px;
  border-radius: 20px;
}

#scanButton {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: auto;
  margin-right: auto;
  text-align: center;

  background-color: #007BFF;
  color: #fff;
  border: 1px rgb(0, 0, 0);
  border-radius: 15px;
  padding: 10px;
  cursor: pointer;
  font-size: 16px;
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
}</style>
