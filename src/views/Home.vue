<template>
  <div class="home">
  
      <div class="row">
        <div v-for="post in posts" class="col-md-4 mb-2">
          <div class="card">

            <div class="card-body">
              <h5 class="card-title">{{ post.title }}</h5>
              <p class="card-text"> {{ post.body }}</p>

            </div>
              <!-- Button trigger modal -->
<button v-on:click="setCurrentPost(post)" type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal">
  Show Entire blog post
</button>

<!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        {{ currentPost.body }}
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div>
          </div>

        </div>
      </div>
      <div class="modal" tabindex="-1" role="dialog">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">{{ currentPost.title}}</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        {{ currentPost.body }}
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
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
        currentPost: {},
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
    methods: {
      setCurrentPost: function(inputPost) {
        this.currentPost = inputPost;
      }
    },
    computed: {}
};
</script>