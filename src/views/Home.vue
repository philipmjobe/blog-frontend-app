<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <h2>All Posts:</h2>
    <div v-for="post in posts" :key="post.id">
      <h3>{{ post.title }}</h3>
      <img :src="post.image" :alt="post.title" />
      <button v-on:click="showPost(post)">More Info</button>
    </div>
    <dialog id="post-details">
      <form method="dialog">
        <h1>Post Info:</h1>
        <p>
          Title:
          <input type="text" v-model="currentPost.title" />
        </p>
        <p>
          Body:
          <input type="text" v-model="currentPost.body" />
        </p>
        <button v-on:click="updatePost(currentPost)">Update Post</button>
        <button v-on:click="destroyPost(currentPost)">Delete</button>
        <button>close</button>
      </form>
    </dialog>
  </div>
</template>

<style>
img {
  width: 250px;
}
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to the blog!!!!",
      posts: [],
      newPostParams: {},
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
    createPost: function () {
      console.log("Making a New Post!");
      axios
        .post("/post", this.newPostParams)
        .then((response) => {
          console.log("Success!", response.data);
          this.posts.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
    showPost: function (post) {
      console.log(post);
      this.currentPost = post;
      document.querySelector("#post-details").showModal();
    },
    updatePost: function (post) {
      axios.patch("/posts/" + post.id, post).then((response) => {
        console.log("Success", response.data);
      });
    },
    destroyPost: function (post) {
      axios.delete("/posts/" + post.id).then((response) => {
        console.log("Success!", response.data);
        var index = this.posts.indexOf(post);
        this.posts.splice(index, 1);
      });
    },
  },
};
</script>
