<template>
  <div class="card">
    <div class="card-header">
      <router-link to="/create" class="btn btn-primary float-right">Create</router-link>
    </div>

    <div class="card-body">
      <table class="table">
        <thead>
          <tr>
            <th>Title</th>
            <th>Description</th>
            <th width="100"></th>
            <th width="100"></th>
            <th width="100"></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="post, index in posts">
            <td>{{post.title}}</td>
            <td>{{post.description}}</td>

            <td>
              <router-link :to="{name:'readPost', params:{id:post.id}}" class="btn btn-info">View</router-link>
            </td>
            <td>
              <router-link :to="{name:'editPost', params:{id:post.id}}" class="btn btn-success">Edit</router-link>
            </td>
            <td>
              <button class="btn btn-danger" v-on:click="deletePost(post.id, index)">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import swal from "sweetalert";
export default {
  data() {
    return {
      posts: [],
      errors: []
    };
  },

  created() {
    axios
      .get(`/posts`)
      .then(response => {
        // JSON responses are automatically parsed.
        this.posts = response.data;
      })
      .catch(e => {
        this.errors.push(e);
      });
  },

  methods: {
    deletePost(id, index) {
      swal({
        title: "Are you sure?",
        text:
          "Once deleted, you will not be able to recover this imaginary file!",
        icon: "warning",
        buttons: true,
        dangerMode: true
      }).then(willDelete => {
        if (willDelete) {
          // swal("Poof! Your imaginary file has been deleted!", {
          //   icon: "success"
          // });
          axios
            .delete("/posts/" + id)
            .then(res => {
              this.posts.splice(index, 1);
            })
            .catch(e => {
              this.errors.push(e);
            });
        } else {
          swal("Your imaginary file is safe!");
        }
      });
    }
  }
};
</script>