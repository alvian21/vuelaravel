<template>
  <div class="container">
    <div class="card">
      <div class="card-header">Edit Post</div>
      <div class="card-body">
        <form v-on:submit="submitPost()">
          <div class="form-group">
            <input
              type="text"
              name
              id
              v-model="posts.title"
              class="form-control"
              placeholder="Judul"
            />
          </div>
          <div class="form-group">
            <textarea
              name
              id
              rows="5"
              v-model="posts.description"
              class="form-control"
              placeholder="Deskripsi"
            ></textarea>
          </div>
          <div class="form-group" style="text-align:center">
            <button class="btn btn-primary">Update</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      posts: {
        title: "",
        description: ""
      },
      errors: []
    };
  },

  // Fetches posts when the component is created.
  created() {
    let id = this.$route.params.id;
    axios
      .get(`/posts/` + id + `/edit`)
      .then(response => {
        console.log(response);

        // JSON responses are automatically parsed.
        this.posts = response.data;
      })
      .catch(e => {
        this.errors.push(e);
      });
  },

  methods: {
    submitPost() {
      let id = this.$route.params.id;
      axios
        .put(`/posts/` + id, this.posts)
        .then(response => {
          //   console.log(response);
          this.$router.push({ path: "/" });
          // JSON responses are automatically parsed.
          this.posts = response.data;
        })
        .catch(e => {
          this.errors.push(e);
        });
    }
  }
};
</script>
