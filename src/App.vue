<template>
  <div>
    <div v-if="flag" style="margin-top:1rem;">
      <div class="card" style="width: 18rem;">
        <div class="card-header">
          <h3><b style="color: violet;">Comments</b></h3>
        </div>
        <ul class="list-group list-group-flush">
          <li v-for="comment in comments" :key="comment.id" class="list-group-item" style="border-bottom:0.5rem">
            <p><b>ID: </b>{{ comment.postId }}</p>
            <p><b>UserId: </b>{{ comment.id }}</p>
            <p><b>Body: </b>{{comment.body}}</p>
            <p style="padding-top: 0.5rem;"><b>Username: </b>{{ comment.user.username }}</p>
            <hr>
          </li>
        </ul>
      </div>
    </div>
    <h2 style="color:darkblue">POSTS TABLE</h2>
    <hr>

    <table class="table table-striped" style="margin-top: 1rem;">
      <thead>
        <tr>
          <th scope="col">ID</th>
          <th scope="col-3">Title</th>
          <th scope="col-6">Body</th>
          <th scope="col">UserID</th>
          <th scope="col">Comments</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="post in posts" :key="post.id">
          <td >{{post.id}}</td>
          <td >{{post.title}}</td>
          <td  style="width:300px">{{post.body}}</td>
          <td >{{post.userId}}</td>
          <td >
            <button type="button" @click="postDataById(post.id)" class="btn btn-primary btn-sm">Show</button>
          </td>
        </tr>
      </tbody>
    </table>
    
  </div>
</template>


<script>
import axios from 'axios';
import 'bootstrap/dist/css/bootstrap.min.css'; // Import Bootstrap CSS
import 'bootstrap/dist/js/bootstrap.bundle.min.js'; // Import Bootstrap JS (Optional for Bootstrap JS components)

export default {
  name: 'App',
  data(){
    return {
      get_api_data:[],
      posts: [],
      comments: [],
      data_by_id: [],
      flag: false
    }
  },
  mounted(){
    this.getDataFromAPI()
  },
  methods:{
    async getDataFromAPI(){
      this.get_api_data = await axios.get('https://dummyjson.com/posts');
      this.posts = this.get_api_data.data.posts;
      console.log('posts',this.posts)
    },
    async postDataById(postId){
      this.data_by_id = await axios.get(`https://dummyjson.com/posts/${postId}/comments`);
      this.comments = this.data_by_id.data.comments;
      this.flag = true
      console.log('hi',this.comments)
    },

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>