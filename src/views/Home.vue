<template>
  <div class="home">
  
      <div class="row">
        <div v-for="post in posts" class="col-md-4 mb-2">
          <div class="card">

            <div class="card-body">
              <h5 class="card-title">{{ post.title }}</h5>
              <p class="card-text">body: {{ post.body }}</p>

            </div>
              <a v-bind:href="'/#/posts/' + post.id" class="btn btn-primary">Show blog</a>
          </div>

        </div>
      </div>
  </div>
</template>

<style>
</style>

<script>
  let axios = require("axios");
export default {
    data: function() {
      return {
        message: "Welcome to Vue.js!",
        posts: [],
        title: "",
        body: ""
      };
    },
    created: function() {
      axios.get("http://localhost:3000/api/posts").then(
        function(response) {
          console.log(response.data);
          this.posts = response.data;
        }.bind(this)
      );
    },
    methods: {},
    computed: {}
};
</script>