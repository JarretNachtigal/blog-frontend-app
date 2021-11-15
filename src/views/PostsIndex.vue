<template>
  <div class="postsIndex">
    <h1>{{ message }}</h1>
    <div>
      <div v-for="post in posts" :key="post.id">
        <h2>{{ post.title }}</h2>
        <p>from user: {{ post.user_id }}</p>
        <p>{{ post.body }}</p>
        <router-link v-bind:to="`posts/${post.id}`">
          <img :src="post.image" :alt="post.title" />
        </router-link>
      </div>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "All Posts",
      posts: [],
    };
  },
  created: function () {
    this.showPosts();
  },
  methods: {
    showPosts: function () {
      axios.get("/posts").then((response) => {
        this.posts = response.data;
        console.log(response);
      });
    },
  },
};
</script>
