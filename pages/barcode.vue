<template>
  <div id="wrapper">
    <v-toolbar color="transparent" absolute width="100%" elevation="0">
      <v-toolbar-title
        ><v-icon left>mdi-barcode</v-icon> Scan Bar code</v-toolbar-title
      >
      <v-spacer></v-spacer>
      <!-- <v-btn icon @click="openFile">
        <v-icon>mdi-file</v-icon>
      </v-btn> -->
      <v-btn icon @click="help = true"><v-icon>mdi-help</v-icon></v-btn>
    </v-toolbar>

    <v-row align="center" justify="center" class="fill-height">
        <StreamBarcodeReader
      v-if="streamActivated && !open"
      height="100vh"
      width="100vw"
      color="primary"
      @decode="onDecode"
      @loaded="onLoaded"
    >
    </StreamBarcodeReader>
      </v-row>

    <!-- <ImageBarcodeReader
      @decode="onDecode"
      @error="onError"
      @selectedImage="showSelectedImage"
      :canselect="open"
    ></ImageBarcodeReader> -->

    <v-row
      v-if="showResult && scannedImage == ''"
      class="fill-height"
      align="center"
      justify="center"
    >
      <v-card color="transparent" elevation="0">
        <v-icon color="#fff" size="110">mdi-qrcode</v-icon>
      </v-card>
    </v-row>

    <img v-if="scannedImage != ''" :src="scannedImage" id="selcimage" />

    <v-bottom-sheet inset v-model="showResult" max-width="500" scrollable>
      <v-card>
        <v-card-title
          >Result <v-spacer></v-spacer>
          <v-btn icon dark large @click="copyToClipboard">
            <v-icon>mdi-content-copy</v-icon>
          </v-btn></v-card-title
        >
        <v-divider></v-divider>
        <v-card-text>
          {{ data }}
        </v-card-text>
        <br />
      </v-card>
    </v-bottom-sheet>

    <v-dialog v-model="help" max-width="500px" transition="dialog-transition">
      <v-card dark>
        <br />
        <v-card-text>
          Place the Qrcode Front of your device Camera to Scan automatically
        </v-card-text>
      </v-card>
    </v-dialog>

    <v-snackbar v-model="copied"> Copied </v-snackbar>
  </div>
</template>

<script>
import { StreamBarcodeReader } from "vue-barcode-reader";
export default {
  components: { StreamBarcodeReader },
  data() {
    return {
      streamActivated: true,
      data: "",
      showResult: false,
      copied: false,
      help: false,
      open: false,
      scannedImage: "",
    };
  },
  methods: {
    onLoaded() {},
    onError(err) {
      setTimeout(() => {
        this.scannedImage = ""; //slow cleanup
      }, 300);
    },
    onDecode(result) {
      this.data = JSON.stringify(result, 2, null);
      //console.log(result);
      this.streamActivated = false;
      this.showResult = true;
    },

    copyToClipboard() {
      var copyFrom = document.createElement("textarea");
      copyFrom.setAttribute(
        "style",
        "position:fixed;opacity:0;top:100px;left:100px;"
      );
      copyFrom.value = this.data;
      document.body.appendChild(copyFrom);
      copyFrom.select();
      document.execCommand("copy");
      this.copied = true;
      setTimeout(function () {
        document.body.removeChild(copyFrom);
        document.body.removeChild(copied);
      }, 1500);
    },
    openFile() {
      this.open = true;
      setTimeout(() => {
        this.open = false;
      }, 700);
    },
    showSelectedImage(res) {
      // console.log(res)
      this.scannedImage = res;
      this.open = false;
    },
  },
  watch: {
    showResult(value) {
      if (!value) {
        this.streamActivated = true;
        this.data = "";
        this.scannedImage = "";
      }
    },
  },
};
</script>

<style>
#wrapper {
  width: 100vw;
  height: 100vh;
}

#selcimage {
  width: 100vw;
  height: 100vh;
  object-fit: contain;
  background-color: #000;
  border: 2px solid red;
}
</style>