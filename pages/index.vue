<template>
  <div id="wrapper">
    <v-carousel
      cycle
      height="100vh"
      hide-delimiter-background
      hide-delimiters
      :show-arrows="false"
    >
      <v-carousel-item>
        <v-sheet height="100%">
          <v-row class="fill-height ma-0" align="center" justify="center">
            <div class="display-1">XcelScanner</div>
          </v-row>
        </v-sheet>
      </v-carousel-item>

      <v-carousel-item>
        <v-sheet height="100%">
          <v-row class="fill-height ma-0" align="center" justify="center">
            <v-card align="center" justify="center" elevation="0">
              <v-btn dark icon width="150" height="150">
                <v-icon size="100">mdi-qrcode</v-icon>
              </v-btn>
              <br />
              QRcode
              <v-card-text>Scan any QRcode with your device camera</v-card-text>
            </v-card>
          </v-row>
        </v-sheet>
      </v-carousel-item>

      <v-carousel-item>
        <v-sheet height="100%">
          <v-row class="fill-height ma-0" align="center" justify="center">
            <v-card align="center" justify="center" elevation="0">
              <v-btn dark icon width="150" height="150">
                <v-icon size="100">mdi-barcode</v-icon>
              </v-btn>
              <br />
              BarCode
              <v-card-text
                >Scan any BarCode with your device camera</v-card-text
              >
            </v-card>
          </v-row>
        </v-sheet>
      </v-carousel-item>

      <v-carousel-item>
        <v-sheet height="100%">
          <v-row class="fill-height ma-0" align="center" justify="center">
            <v-card align="center" justify="center" elevation="0">
              <v-btn dark icon width="80" height="80">
                <v-icon size="50">mdi-image</v-icon>
              </v-btn>

              <v-btn dark icon width="80" height="80">
                <v-icon size="30">mdi-arrow-right-bold</v-icon>
              </v-btn>

              <v-btn dark icon width="80" height="80">
                <v-icon size="50">mdi-adobe-acrobat</v-icon>
              </v-btn>
              <br />
              <br />
              Image to PDF
              <v-card-text>Convert Any Image to PDf</v-card-text>
            </v-card>
          </v-row>
        </v-sheet>
      </v-carousel-item>
    </v-carousel>

    <v-btn width="60" height="60" id="begin" light fab @click="showMore = true">
      <v-icon>mdi-plus</v-icon>
    </v-btn>

    <v-bottom-sheet inset v-model="showMore" max-width="500">
      <v-card>
        <v-card-text>
          <v-row>
            <v-col
              @click="open('/qrcode')"
              cols="4"
              align="center"
              justify="center"
            >
              <v-btn dark icon width="50" height="50">
                <v-icon size="30">mdi-qrcode</v-icon>
              </v-btn>
              <br />
              QRcode
            </v-col>
            <v-col
              @click="open('/barcode')"
              cols="4"
              align="center"
              justify="center"
            >
              <v-btn dark icon width="50" height="50">
                <v-icon size="30">mdi-barcode</v-icon>
              </v-btn>
              <br />
              Barcode
            </v-col>
            <v-col
              @click="open('pdf')"
              cols="4"
              align="center"
              justify="center"
            >
              <v-btn dark icon width="50" height="50">
                <v-icon size="30">mdi-adobe-acrobat</v-icon>
              </v-btn>
              <br />
              PDF
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
    </v-bottom-sheet>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showMore: false,
    };
  },
  mounted(){
    console.log(this.$device.os_name)
  },
  methods: {
    open(route) {
     this.$router.push(route)
    },
  },
};
</script>

<style lang="scss" scoped>
#wrapper {
  width: 100%;
  height: 100%;
}

#begin {
  position: fixed;
  z-index: 100;
  right: 20px;
  bottom: 20px;
}
</style>