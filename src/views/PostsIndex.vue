<template>
  <div>
    <h1>{{ message }}</h1>

    <div
      v-for="post in posts"
      v-on:click="currentPost = post"
      v-bind:class="{ selected: post === currentPost }"
      :key="post.id"
    >
      <div class="card" style="width: 18rem">
        <img :src="post.image" class="card-img-top" alt="oops" />
        <div class="card-body">
          <h5 class="card-title">{{ post.title }}</h5>
          <p class="card-text">Added: {{ relativeDate(post.created_at) }}</p>
          <p class="card-text">Updated: {{ relativeDate(post.updated_at) }}</p>
          <router-link :to="`/posts/${post.id}`">
            <a class="btn btn-primary">More info</a>
          </router-link>
        </div>
      </div>
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
import moment from "moment";

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
      axios.get("/posts").then((response) => {
        this.posts = response.data;
        console.log("All Posts", this.posts);
      });
    },
    relativeDate: function (date) {
      return moment(date).fromNow();
    },
  },
};
</script>
