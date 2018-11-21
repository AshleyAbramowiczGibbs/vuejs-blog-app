<template>
  <div class="Newpost">
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <h1>New Post</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <label>Blog Post Title:</label> 
          <input type="text" class="form-control" v-model="title">
        </div>
        <div class="form-group">
          <label>Blog Post:</label>
          <input type="textarea" class="form-control" v-model="body">
        </div>
        
        <input type="submit" class="btn btn-primary" value="Submit">
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      title: "",
      body: "",
      errors: []
    };
  },
  methods: {
    submit: function() {
      var params = {
        title: this.title,
        body: this.body,
      };
      axios
        .post("http://localhost:3000/api/posts", params)
        .then(response => {
          this.$router.push("./");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>