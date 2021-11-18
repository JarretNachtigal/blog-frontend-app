<template>
  <div class="postsIndex">
    <h1>{{ message }}</h1>
    <!-- old search bar, new one is in app.vue -->
    Search by Title:
    <input type="text" v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option :key="post.id" v-for="post in posts">{{ post.title }}</option>
    </datalist>
    <button v-on:click="sortAttribute = 'title'">sort by title</button>
    <button v-on:click="sortAttribute = 'body'">sort by body</button>
    <div>
      <!-- can remove/change/add another 'title' -->
      <div v-for="post in orderBy(filterBy(posts, titleFilter, 'title'), sortAttribute)" :key="post.id">
        <div class="row">
          <div class="col-3"></div>
          <div class="col-6">
            <div class="card">
              <div class="card-body" v-on:click="currentPost = post" v-bind:class="{ selected: post === currentPost }">
                <h5 class="card-title">{{ post.title }}</h5>
                <p class="card-text">from user: {{ post.user_id }}</p>
                <p class="card-text">{{ post.body }}</p>
                <p class="card-text">Created: {{ relativeDate(post.created_at) }}</p>
                <p class="card-text">Updated: {{ relativeDate(post.updated_at) }}</p>
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
import moment from "moment";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      message: "All Posts",
      posts: [],
      currentPost: {},
      titleFilter: "",
      sortAttribute: "",
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
    relativeDate: function (date) {
      return moment(date).fromNow();
    },
  },
};
</script>
