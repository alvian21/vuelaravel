<template>
  <div class="container">
    <div class="card">
      <div class="card-header">Show Post</div>
      <div class="card-body">
        <h2>{{posts.title}}</h2>
        <p>{{posts.description}}</p>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data() {
    return {
      posts: [],
      errors: []
    };
  },

  created() {
    let id = this.$route.params.id;
    axios
      .get(`/posts/` + id)
      .then(response => {
        console.log(response);

        // JSON responses are automatically parsed.
        this.posts = response.data;
      })
      .catch(e => {
        this.errors.push(e);
      });
  }
};
</script>