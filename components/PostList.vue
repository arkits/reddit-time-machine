<template>
  <v-container id="postlist" grid-list-md>
    <div v-for="post in getPosts" if="getPosts.length > 0" v-bind:key="post.id">
      <v-layout row wrap>
        <v-flex xs12>
          <PostCard v-bind:post="post" />
        </v-flex>
      </v-layout>
    </div>
  </v-container>
</template>

<script>
import PostCard from "./PostCard";

export default {
  name: "PostList",
  props: ["apiResponse"],
  components: {
    PostCard
  },
  computed: {
    getPosts() {
      try {
        var data = this.apiResponse.data;
      } finally {
      }
      return data;
    }
  }
};
</script>
