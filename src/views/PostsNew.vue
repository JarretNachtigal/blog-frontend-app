<template>
  <div class="postsIndex">
    <h1>{{ message }}</h1>
    <form v-on:submit.prevent="createPost()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="newPostParams.body" />
      </div>
      <div>
        <label>Image Url:</label>
        <input type="text" v-model="newPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Create a New Post",
      newPostParams: {},
      errors: [],
    };
  },
  methods: {
    createPost: function () {
      axios
        .post("/posts", this.newPostParams)
        .then(() => {
          console.log("post created");
          this.$router.push("/posts");
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
