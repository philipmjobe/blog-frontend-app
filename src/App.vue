<template>
  <div class="content">
    <div id="app">
      <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container-fluid">
          <a class="navbar-brand" href="#">Navbar</a>
          <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <a class="nav-link active" aria-current="page" href="/">Home</a>
              </li>
              <li class="nav-item">
                <a v-if="!isLoggedIn()" class="nav-signup" href="/signup">Sign Up</a>
              </li>
              <li class="nav-item" v-if="!isLoggedIn()">
                <a class="nav-link" href="/login">Login</a>
              </li>
              <li class="nav-item" v-if="isLoggedIn()">
                <a class="nav-link" href="/logout">Logout</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/posts">All Posts</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="/posts/new">New Post</a>
              </li>
              <!-- <li class="nav-item dropdown">
                <a
                  class="nav-link dropdown-toggle"
                  href="#"
                  id="navbarDropdown"
                  role="button"
                  data-bs-toggle="dropdown"
                  aria-expanded="false"
                >
                  Sign In/Logout
                </a>
                <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                  <li><a v-if="!isLoggedIn()" class="dropdown-item" href="/login">Sign In</a></li>
                  <li><a v-if="isLoggedIn()" class="dropdown-item" href="/logout">Log Out</a></li>
                </ul>
              </li>
              <li class="nav-item dropdown">
                <a
                  class="nav-link dropdown-toggle"
                  href="#"
                  id="navbarDropdown"
                  role="button"
                  data-bs-toggle="dropdown"
                  aria-expanded="false"
                >
                  Posts
                </a>
                <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                  <li><a class="dropdown-item" href="/posts">All Posts</a></li>
                  <li><a class="dropdown-item" href="/posts/new">Create a Post</a></li>
                </ul>
              </li> -->
            </ul>
            <form class="d-flex">
              <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search" />
              <button class="btn btn-outline-success" type="submit">Search</button>
            </form>
          </div>
        </div>
      </nav>
      <div id="nav"></div>
      <router-view />
    </div>
  </div>
</template>

<style>
body {
  background-image: url(./assets/dark-honeycomb.png);
}

div {
  color: rgb(161, 19, 19);
}

.content {
  max-width: 600px;
  margin: auto;
}
</style>

<script>
export default {
  methods: {
    isLoggedIn: function () {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>
