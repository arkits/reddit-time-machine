<template>
  <v-app dark>
    <center>
      <br />
      <br />
      <h1 class="space-bigger" v-if="error.statusCode === 404">{{ pageNotFound }}</h1>
      <h1 class="space-bigger" v-else>{{ otherError }}</h1>
      <br />
      <br />
      <v-btn class="text-none" x-large href="/reddit-time-machine" color="primary">Come back Home</v-btn>
    </center>
  </v-app>
</template>

<script>
export default {
  layout: "empty",
  props: {
    error: {
      type: Object,
      default: null
    }
  },
  head() {
    const title =
      this.error.statusCode === 404 ? this.pageNotFound : this.otherError;
    return {
      title
    };
  },
  data() {
    return {
      pageNotFound: "Where you going, mate?",
      otherError: "@arkits messed up!"
    };
  }
};
</script>

<style>
.space-bigger {
  font-family: "Space Mono", monospace;
  font-size: 3rem;
}
</style>
