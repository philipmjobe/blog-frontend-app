<template>
  <div class="posts-show">
    <h1>{{ post.title }}</h1>
    <h3>{{ post.title }}</h3>
    <img :src="post.image" :alt="post.title" />
    <router-link to="/">Back to all Posts</router-link>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id).then((resposnse) => {
      this.post = resposnse.data;
    });
  },
  methods: {},
};
</script>
