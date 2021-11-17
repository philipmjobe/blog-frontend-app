<template>
  <div class="posts-new">
    <img v-if="status" :src="`http://http.cat/${status}`" alt="" />
    <form v-on:submit.prevent="createPost()">
      <h1>New Post!</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Tilte:</label>
        <input type="text" v-model="newPostParams.title" />
      </div>
      <div>
        <label>Post:</label>
        <input type="text" v-model="newPostParams.body" />
        <small v-if="newPostParams.body.length > 0 && newPostParams.body.length < 6" class="text-danger">
          Must be at least 6 characters
        </small>
        <small v-if="newPostParams.body.length < 20" class="text-danger">No more than 20 characters please.</small>
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="newPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newPostParams: { body: "" },
      errors: [],
      status: "",
    };
  },
  methods: {
    createPost: function () {
      console.log("Making a post!");

      axios
        .post("/posts", this.newPostParams)
        .then(() => {
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.status = error.response.status;
          console.log(error.response);
        });
    },
  },
};
</script>
