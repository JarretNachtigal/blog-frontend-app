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
        <!-- <input type="text" class="form-control is-invalid" v-model="newPostParams.title" /> -->
        <small v-if="newPostParams.title.length < 6 && newPostParams.title.length > 0" class="text-danger">
          title must be at least 6 characters
        </small>
        <small v-if="newPostParams.title.length > 6 && newPostParams.title.length < 20">
          {{ 20 - this.newPostParams.title.length }} characters remaining
        </small>
        <small v-if="newPostParams.title.length > 6 && newPostParams.title.length > 20" class="text-danger">
          title must be less than 20 characters
        </small>
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="newPostParams.body" />
        <small v-if="newPostParams.body.length < 6 && newPostParams.body.length > 0" class="text-danger">
          body must be at least 6 characters
        </small>
        <small v-if="newPostParams.body.length > 6 && newPostParams.body.length < 300">
          {{ 300 - this.newPostParams.body.length }} characters remaining
        </small>
        <small v-if="newPostParams.body.length > 300" class="text-danger">
          body must be at less than 300 characters
        </small>
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
      newPostParams: { title: "", body: "", image: "" },
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
