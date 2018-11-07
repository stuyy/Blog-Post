<template lang="html">
  <div>
    <b-nav tabs>
      <b-nav-item v-on:click="navigate('create')">Create a Post</b-nav-item>
      <b-nav-item v-on:click="navigate('view')">View Posts</b-nav-item>
    </b-nav>
    <CreatePost v-if="showCreate"/>
    <ViewPost ref="views" v-if="showView"/>
  </div>
</template>

<script>

import CreatePost from './CreatePost'
import ViewPost from './ViewPost'
export default {
  name: 'Navbar',
  components: {
    CreatePost, ViewPost
  },
  data () {
    return {
      showCreate: false,
      showView: false
    }
  },
  methods: {
    navigate(endpoint)
    {
      if(endpoint == 'create')
      {
        this.showCreate = true;
        this.showView = false;
        this.$parent.showParentCreate = false;
      }
      else if(endpoint == 'view')
      {
        this.showView = true;
        this.showCreate = false;
        this.$parent.showParentCreate = false;
      }
    }
  }
}
</script>

<style lang="css">
</style>
