<template lang="html">
  <div class="create container">
    <h1 class="h1-title">Create a Post</h1>
    <b-alert v-if="postCreated" variant="success" show>Post successfully made</b-alert>
    <b-alert v-if="postError" variant="danger" show>Error trying to post...</b-alert>
    <b-form @submit.prevent="createPost">
      <b-form-input class="mt-3" type="text" placeholder="Your Name" v-model="name" name="name" required></b-form-input>
      <b-form-input class="mt-3" type="text" placeholder="Subject" v-model="subject" name="subject" required></b-form-input>
      <b-form-textarea class="mt-3 mb-3" type="text" placeholder="Your Post":rows="3" :max-rows="6" v-model="message" name="message" required></b-form-textarea>
      <b-button type="submit" value="Submit" variant="primary" style="float: right"><i class="fas fa-plus"></i> Create Blog Post</b-button>
    </b-form>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'CreatePost',
  data () {
    return {
      name: '',
      subject: '',
      message: '',
      postCreated: false,
      postError: false
    }
  },
  methods: {
    createPost() {
      axios.post('http://localhost:3000/post', {
        name: this.name,
        subject: this.subject,
        message: this.message
      })
      .then(post => {
        this.postCreated = true;
        this.postError = false;
        this.name = this.subject = this.message = '';
      })
      .catch(err => {
        this.postError = true;
        this.postCreated = false;
        console.log("False");
      });

      setTimeout(() => {
        this.postCreated = false;
        this.postError = false;
      }, 5000);
    }
  }
}
</script>

<style lang="css">
.h1-title {
  text-align: left;
  padding-top: 10px;
}
.create {
  margin-top: 50px;
}
</style>
