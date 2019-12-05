<template>
  <v-card class="mx-auto" dark :href="post.full_link">
    <v-card-text class="white--text">
      <div class="space-font">{{post.title}}</div>
      <div class="font-italic grey--text">{{post.selftext.substring(0, 200)}}</div>
      <v-row no-gutters>
        <v-col class="font-italic grey--text text--lighten-2" cols="10">/u/{{post.author}}</v-col>
        <v-col cols="1"> <v-icon>mdi-thumb-up</v-icon> {{post.score}}</v-col>
        <v-col cols="1"> <v-icon>mdi-message</v-icon> {{post.num_comments}}</v-col>
      </v-row>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  name: "PostCard",
  props: ["post"]
};
</script>
<style scoped>
.space-font{
  font-size: 1.2rem;
}
</style>
