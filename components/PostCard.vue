<template>
  <v-card class="mx-auto" dark :href="post.full_link">
    <v-card-title  class="headline font-weight-light">{{post.title}}</v-card-title>
    <v-card-text>{{post.selftext}}</v-card-text>
    <v-card-actions>
      <v-list-item class="grow">
        <v-list-item-content>
          <v-list-item-title>{{post.author}}</v-list-item-title>
        </v-list-item-content>
        <v-row align="center" justify="end">
          <v-icon class="mr-1">mdi-thumb-up</v-icon>
          <span class="subheading mr-2">{{post.score}}</span>
          <span class="mr-1">·</span>
          <v-icon class="mr-1">mdi-message</v-icon>
          <span class="subheading">{{post.num_comments}}</span>
        </v-row>
      </v-list-item>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "PostCard",
  props: ["post"]
};
</script>
