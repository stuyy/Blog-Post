<template lang="html">
  <div class="main container">
    <Navbar/>
    <CreatePost v-if="showParentCreate"/>
  </div>
</template>

<script>
import Navbar from './addons/Navbar'
import CreatePost from './addons/CreatePost'
import ViewPost from './addons/ViewPost'
export default {
  name: 'Main',
  components: {
    Navbar, CreatePost
  },
  data () {
    return {
      showParentCreate: true
    }
  },
  methods: {
    callFetchPosts()
    {
        ViewPost.fetchPosts()
    }
  }
}
</script>

<style lang="css">
.main {
  width: 80%;
  margin: 0 auto;

}
</style>
