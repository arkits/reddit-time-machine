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
                  <v-text-field v-model="startDate" label="Start Date" readonly v-on="on"></v-text-field>
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
                  <v-text-field v-model="endDate" label="End Date" readonly v-on="on"></v-text-field>
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

    <div v-if="inputError">
      <v-alert type="error">{{inputError}}</v-alert>
    </div>

    <div v-if="inputSuccess">
      <v-alert type="success">{{inputSuccess}}</v-alert>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ApiParamsForm",
  data() {
    return {
      subredditName: "pcgaming",
      inputError: "",
      inputSuccess: "",
      startDate: new Date().toISOString().substr(0, 10),
      startDateMenu: false,
      endDate: new Date().toISOString().substr(0, 10),
      endDateMenu: false
    };
  },
  methods: {
    doTheTing: function() {
      var vm = this;

      console.log(this.subredditName);
      console.log(this.startDate);
      console.log(this.endDate);

      var url = "https://api.pushshift.io/reddit/submission/search/?";

      url = url + "&subreddit=" + this.subredditName;

      axios
        .get(url)
        .then(function(response) {
          vm.inputSuccess = response.data;
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