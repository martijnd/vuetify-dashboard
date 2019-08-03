<template>
  <v-app>
    <Navbar @newQuote="fetchQuote" />
    <v-layout align-center justify-center column>
      <blockquote class="blockquote">{{ quote }}</blockquote>
    </v-layout>
    <v-snackbar color="deep-purple accent-4" v-model="snackbar">
      Fetched new quote
      <v-btn color="white" text @click="snackbar = false">Close</v-btn>
    </v-snackbar>
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
      dialog: false,
      snackbar: false,
      index: 0
    };
  },
  methods: {
    fetchQuote() {
      this.snackbar = true;
      const data = {
        index: this.index
      };
      const config = {
        headers: {
          "Content-Type": "application/json"
        }
      };

      this.different = false;
      axios
        .post("https://inspire.martijnd.workers.dev", data, config)
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