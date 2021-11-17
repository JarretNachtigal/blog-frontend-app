<template>
  <div class="postsIndex">
    <h1>{{ message }}</h1>
    <div>
      <div v-for="post in posts" :key="post.id">
        <div class="row">
          <div class="col-3"></div>
          <div class="col-6">
            <div class="card">
              <div class="card-body" v-on:click="currentPost = post" v-bind:class="{ selected: post === currentPost }">
                <h5 class="card-title">{{ post.title }}</h5>
                <p class="card-text">from user: {{ post.user_id }}</p>
                <p class="card-text">{{ post.body }}</p>
                <router-link v-bind:to="`posts/${post.id}`">
                  <img :src="post.image" :alt="post.title" />
                </router-link>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
img {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 40%;
}
h1 {
  text-align: center;
}
.selected {
  background-color: red;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "All Posts",
      posts: [],
      currentPost: {},
      // highlighted: false,
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
