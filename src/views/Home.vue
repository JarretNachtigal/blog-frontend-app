<template>
  <div class="home">
    <p>{{ message }}</p>
    <p></p>
  </div>
</template>

<script>
import axios from "axios";

axios.defaults.baseURL = process.env.NODE_ENV === "development" ? "http://localhost:3000" : "/";

export default {
  data: function () {
    return {
      message: "hello from vue",
      posts: [],
    };
  },
  created: function () {},
  methods: {},
};
</script>
