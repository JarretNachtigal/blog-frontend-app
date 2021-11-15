<template>
  <div class="postsShow">
    <h1>{{ post.title }}</h1>
    <div>
      <p>from user: {{ post.title }}</p>
      <p>{{ post.body }}</p>
      <img :src="post.image" :alt="post.title" />
      <router-link to="/posts">back to all</router-link>
      |
      <router-link v-bind:to="`/posts/${post.id}/edit`">edit</router-link>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Post",
      post: {},
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id).then((response) => {
      this.post = response.data;
      console.log(response);
    });
  },
  methods: {},
};
</script>
