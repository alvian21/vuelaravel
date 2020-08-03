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
          <tr v-for="post of posts">
           <td>{{post.title}}</td>
            <td>{{post.description}}</td>
         
            <td>   <router-link :to="{name:'readPost', params:{id:post.id}}" class="btn btn-info">View</router-link></td>
            <td><button class="btn btn-success">Edit</button></td>
            <td><button class="btn btn-danger">Delete</button></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
import axios from 'axios';

export default {
  data() {
    return {
      posts: [],
      errors: []
    }
  },


  created() {
    axios.get(`/posts`)
    .then(response => {
      // JSON responses are automatically parsed.
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>