<template>
  <div>
    <h1>{{ message }}</h1>
    <div
      v-for="post in posts"
      v-on:click="currentPost = post"
      v-bind:class="{ selected: post === currentPost }"
      :key="post.id"
    >
      <h3>{{ post.title }}</h3>
      <router-link v-bind:to="`/posts/${post.id}`">
        <img :src="post.image" :alt="post.title" />
      </router-link>
    </div>
  </div>
</template>

<style>
.selected {
  color: orange;
  background-color: black;
  transition: background-color 3s ease;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to the blog!",
      posts: [],
      currentPost: {},
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
