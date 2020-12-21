<template>
  <v-app dark>
    <nuxt />
  </v-app>
</template>

<script>
export default {
  data() {
    return {};
  },
  mounted() {
    let eHtml = document.getElementsByTagName("html")[0];
    eHtml.style.overflowY = "hidden";
  },
};
</script>
