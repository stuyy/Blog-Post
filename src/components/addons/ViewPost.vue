<template lang="html">
  <div class="post-body">
    <h1 class="title">Recent Posts</h1>
    <b-alert show variant="info" v-if="postDeleted">Post Deleted</b-alert>
    <div v-for="post in posts" class="message">
      <i v-on:click="deletePost" class="fas fa-times fa-2x icon-close" id="close"></i>
      <h2>{{post.subject}}</h2>
      <p><span class="author">By {{post.name}}</span> on <span class="date">{{post.createdAt}}</span></p>
      <p>{{post.message}}</p>
    </div>
  </div>
</template>

<script>

import axios from 'axios'
export default {
  name: 'ViewPost',
  components: {

  },
  data () {
    return {
      posts: [],
      currentPost: '',
      postDeleted: false
    }
  },
  methods: {
    fetchPosts()
    {
      axios.get('https://blogpostvue.herokuapp.com/post')
      .then(result => {
        this.posts = result.data;
        var i = 0;
        while(i<this.posts.length)
        {
          console.log(this.posts[i].name);
          console.log(this.posts[i].subject);
          console.log(this.posts[i].message);
          var d = new Date(this.posts[i].createdAt);
          this.posts[i].createdAt = d.toLocaleString()
          i++;
        }
      })
      .catch(err => console.log(err));
    },
    deletePost(e)
    {
      console.log("Hey");
      var currentPost = e.target.nextSibling.nextSibling.nextSibling.nextSibling.nextSibling.nextSibling.innerText;
      var i = 0;
      var deletePostObject = {
        name: '',
        subject: '',
        message: ''
      }
      for(i = 0; i<this.posts.length; i++)
        if(this.posts[i].message === currentPost)
        {
          deletePostObject.name = this.posts[i].name;
          deletePostObject.subject = this.posts[i].subject;
          deletePostObject.message = this.posts[i].message;
          break;
        }
      console.log(deletePostObject);
      axios.delete('https://blogpostvue.herokuapp.com/post', {
        data: deletePostObject
      })
      .then(status => {
        this.postDeleted = true;
        this.fetchPosts();
      })
      .catch(err => {
        console.log("Error!");
      });
      setTimeout(()=> {
        this.postDeleted = false;
      }, 5000)
    }
  },
  mounted () {
    this.fetchPosts();
  }
}



</script>

<style lang="css">
.post-body {
  margin-top: 50px;
  border-radius: 25px;
}
.title {
  text-align: left;
  padding: 20px;
}

.author {

}

.date {

}
.icon-close {
  color: red;
  float: right;
}
#close {

}
.message {
  text-align: left;
  padding: 20px;
  border-top-style: solid;
  border-top-width: 1.5px;
}
</style>
