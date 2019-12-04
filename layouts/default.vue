<template>
  <v-app dark>
    <v-app-bar fixed app>
      <v-toolbar-title v-text="title" class="text-center space-font" />
    </v-app-bar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <v-footer absolute class="font-weight-medium">
      <v-col class="text-center" cols="12">
        <strong class="space-italics">@arkits</strong>
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
.space-font{
  font-family: 'Space Mono', monospace;
  font-style: italic;
  font-weight: 700;
  font-size: 1.5rem;
}
.space-italics{
  font-family: 'Space Mono', monospace;
  font-style: italic;
}
</style>