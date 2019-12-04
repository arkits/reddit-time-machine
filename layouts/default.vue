<template>
  <v-app dark>
    <v-app-bar fixed app>
      <v-toolbar-title class="text-center">
                  <span>
                <a href="/reddit-time-machine" class="app-title white--text">reddit time machine</a>
            </span>
      </v-toolbar-title>
    </v-app-bar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <v-footer absolute class="font-weight-medium">
      <v-col class="text-center" cols="12">
        <strong class="app-footer">@arkits</strong>
      </v-col>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      title: 'reddit time machine'
    }
  }
}
</script>
<style>
.app-title {
    font-family: 'Space Mono', monospace;
    font-style: italic;
    text-decoration: none;
    font-size: 2rem;
}

.app-footer {
    font-family: 'Space Mono', monospace;
    font-style: italic;
    text-decoration: none;
}
</style>