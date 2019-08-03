<template>
  <v-app>
    <Navbar />
    <v-layout align-center justify-center column>
      <p>{{ quote}}</p>
      <v-btn @click="fetchQuote" color="primary">New quote</v-btn>
    </v-layout>
  </v-app>
</template>
<script>
import axios from "axios";

import Navbar from "./components/Navbar.vue";

export default {
  components: {
    Navbar
  },
  name: "App",
  data() {
    return {
      quote: "Loading...",
      index: 0
    };
  },
  methods: {
    fetchQuote() {
      this.different = false;
      axios
        .post(
          "https://inspire.martijnd.workers.dev",
          {
            index: this.index
          },
          {
            headers: {
              "Content-Type": "application/json"
            }
          }
        )
        .then(res => {
          this.quote = res.data.quote;
          this.index = res.data.index;
        });
    }
  },

  mounted() {
    this.fetchQuote();
  }
};
</script>