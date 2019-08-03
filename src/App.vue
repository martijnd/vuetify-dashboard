<template>
  <v-app>
    <v-card class="mx-auto overflow-hidden" height="400" width="344">
      <v-system-bar color="deep-purple darken-3"></v-system-bar>
      <Navbar />
    </v-card>
  </v-app>
</template>
<script lang="ts">
import Navbar from "./components/Navbar.vue";

export default {
  components: {
    Navbar
  },
  name: "App",
  data() {
    return {};
  },

  mounted() {}
};
</script>