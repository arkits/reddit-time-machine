<template>
  <div>
    <v-container>
      <v-form ref="apiParamsForm">
        <v-row>
          <v-col>
            <v-text-field
              outlined
              v-model="subredditName"
              name="input-subredditname"
              label="Subreddit Name"
              hint="Enter a subreddit name."
            ></v-text-field>
          </v-col>
          <v-col>
            <v-menu
              v-model="startDateMenu"
              :close-on-content-click="false"
              :nudge-right="40"
              transition="scale-transition"
              offset-y
              min-width="290px"
            >
              <template v-slot:activator="{ on }">
                <v-text-field v-model="startDate" label="Start Date" outlined readonly v-on="on"></v-text-field>
              </template>
              <v-date-picker v-model="startDate" @input="startDateMenu = false"></v-date-picker>
            </v-menu>
          </v-col>
          <v-col>
            <v-menu
              v-model="endDateMenu"
              :close-on-content-click="false"
              :nudge-right="40"
              transition="scale-transition"
              offset-y
              min-width="290px"
            >
              <template v-slot:activator="{ on }">
                <v-text-field outlined v-model="endDate" label="End Date" readonly v-on="on"></v-text-field>
              </template>
              <v-date-picker v-model="endDate" @input="endDateMenu = false"></v-date-picker>
            </v-menu>
          </v-col>
          <v-col>
            <v-btn block large color="green" @click="doTheTing">Go!</v-btn>
          </v-col>
        </v-row>
      </v-form>
    </v-container>

    <div v-if="isLoading">
      <v-progress-linear indeterminate color="yellow darken-2"></v-progress-linear>
    </div>

    <div v-if="inputError">
      <v-alert type="error">{{inputError}}</v-alert>
    </div>

    <PostList v-bind:apiResponse="apiResponse" />

  </div>
</template>

<script>
import axios from "axios";
import PostList from "../components/PostList";

export default {
  name: "ApiParamsForm",
  components: {
    PostList
  },
  data() {
    return {
      subredditName: "pcgaming",
      inputError: "",
      apiResponse: "",
      startDate: new Date(new Date().setDate(new Date().getDate()-1)).toISOString().substr(0, 10),
      startDateMenu: false,
      endDate: new Date().toISOString().substr(0, 10),
      endDateMenu: false,
      isLoading: false
    };
  },
  methods: {
    doTheTing: function() {
      var vm = this;

      this.isLoading = true;

      var url = "https://api.pushshift.io/reddit/submission/search/?";

      url = url + "&subreddit=" + this.subredditName;
      url = url + "&after=" + new Date(this.startDate).getTime() / 1000;
      url = url + "&before=" + new Date(this.endDate).getTime() / 1000;
      url = url + "&sort_type=" + "score";
      url = url + "&sort=" + "desc";

      console.log(url);

      axios
        .get(url)
        .then(function(response) {
          vm.isLoading = false;
          vm.apiResponse = response.data;
          console.log(response.data);
        })
        .catch(function(error) {
          console.log(error);
          vm.inputError = error;
        });
    }
  },
  watch: {
    dialog: function() {
      this.inputError = "";
      this.inputSuccess = "";
      this.$refs.operationAdderForm.reset();
    }
  }
};
</script>