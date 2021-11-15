<template>
  <div class="postsEdit">
    <form v-on:submit.prevent="updatePost()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="currentPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="currentPostParams.body" />
      </div>
      <div>
        <label>Image Url:</label>
        <input type="text" v-model="currentPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
    </form>
    <button v-on:click="destroyPost()">delete</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      currentPostParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      this.currentPostParams = response.data;
    });
  },
  methods: {
    updatePost: function () {
      axios.patch(`/posts/${this.$route.params.id}`, this.currentPostParams).then((response) => {
        console.log(response.data);
        this.$router.push("/posts");
      });
    },
    destroyPost: function () {
      axios.delete(`/posts/${this.$route.params.id}`).then((response) => {
        console.log("deleted", response.data);
        this.$router.push("/posts");
      });
    },
  },
};
</script>
