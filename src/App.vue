<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/signup">Signup</router-link>
      |
      <router-link to="/login">Login</router-link>
      |
      <router-link to="/logout">Logout</router-link>
      |
      <router-link to="/posts/new">New Posts</router-link>
    </div> -->
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="/">Home</a>
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
              <a class="nav-link" href="/about">About</a>
            </li>
            <li v-if="isLoggedIn()" class="nav-item">
              <a class="nav-link" href="/posts/new">Create Post</a>
            </li>
            <li v-if="!isLoggedIn()" class="nav-item">
              <a class="nav-link" href="/login">Login</a>
            </li>
            <li v-if="isLoggedIn()" class="nav-item">
              <a class="nav-link" href="/logout">Log out</a>
            </li>
            <li v-if="!isLoggedIn()" class="nav-item">
              <a class="nav-link" href="/signup">Sign up</a>
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
                Dropdown
              </a>
              <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                <li><a class="dropdown-item" href="#">Action</a></li>
                <li><a class="dropdown-item" href="#">Another action</a></li>
                <li><hr class="dropdown-divider" /></li>
                <li><a class="dropdown-item" href="#">Something else here</a></li>
              </ul>
            </li> -->

            <!-- <li class="nav-item">
              <a class="nav-link disabled">Disabled</a>
            </li> --->
          </ul>
          <form class="d-flex">
            <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search" />
            <button class="btn btn-outline-success" type="submit">Search</button>
          </form>
        </div>
      </div>
    </nav>
    <div v-on:click="flashMessageReset()" v-if="flashMessage" class="alert alert-success">
      {{ flashMessage }}
    </div>
    <router-view />
  </div>
</template>

<style></style>

<script>
export default {
  data: function () {
    return {
      flashMessage: "",
    };
  },
  methods: {
    isLoggedIn: function () {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
    flashMessageReset: function () {
      this.flashMessage = "";
    },
  },
};
</script>
