<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <v-card>
        <v-card-title class="headline">
          Welcome to the Vuetify + Nuxt.js template
        </v-card-title>
        <v-card-actions>
          <v-spacer />
          <v-btn @click="addOperationToStore">
            Continue
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from 'axios'

export default {
  methods: {
    addOperationToStore: () => {
      console.log('YOLO')
      axios
        .get(
          'https://api.pushshift.io/reddit/submission/search/?after=1334426439&before=1339696839&sort_type=score&sort=desc&subreddit=pcgaming'
        )
        .then(function (response) {
          console.log(response.data)
        })
        .catch(function (error) {
          console.log(error)
        })
    }
  }
}
</script>
