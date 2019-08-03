<template>
  <v-app>
    <Navbar />
    <v-layout align-center justify-center column>
      <v-dialog v-model="dialog" width="500">
        <template v-slot:activator="{ on }">
          <v-btn color="red lighten-2" @click="fetchQuote" dark v-on="on">Click me</v-btn>
        </template>
        <v-card>
          <v-card-title class="headline" primary-title>Quote of the day</v-card-title>
          <v-card-text class="pt-4">{{ quote }}</v-card-text>
          <v-divider></v-divider>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="primary" text @click="dialog = false">Cool stuff</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
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
      dialog: false,
      index: 0
    };
  },
  methods: {
    fetchQuote() {
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