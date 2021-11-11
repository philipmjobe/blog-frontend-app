<template>
  <div>
    <h1>{{ message }}</h1>
    <div v-for="post in posts" v-bind:key="post.id">
      <h3>{{ post.title }}</h3>
      <img :src="post.image" :alt="post.title" />
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to the blog!",
      posts: [],
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("/posts").then((response) => (this.posts = response.data));
      console.log("All Posts", this.posts);
    },
  },
};
</script>
