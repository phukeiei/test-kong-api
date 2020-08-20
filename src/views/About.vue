<template>
  <div class="app">
    <v-form>
      <v-text-field v-model="name" label="Consumer Id or Name"></v-text-field>
      <v-btn color="warning" @click="searchPlugin">Search Plugin</v-btn>
    </v-form>

    <div v-if="jsonAcl">
      <hr />
      <h1>Acl</h1>
      <div></div>
      {{jsonAcl}}
    </div>
    <!-- <div v-if="jsonRoute">
      <hr />
      <h1>Route</h1>
      <div></div>
      {{jsonRoute}}
    </div>-->
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    name: "5da93f42-b1b3-419f-9ff1-b5081bf37095",
    jsonAcl: "",
    jsonRoute: "",
  }),

  methods: {
    async searchPlugin() {
      let res = [];
      await axios
        .get("http://localhost:8001/consumers/" + this.name + "/acls")
        .then(function (response) {
          response.data.data.map((response) => {
            res.push(response);
            console.log(res);
          });
        });
      this.jsonAcl = res;
      // let res2 = [];
      // await axios
      //   .get("http://localhost:8001/plugins/" + this.jsonAcl[0].id + "/route")
      //   .then(function (response) {
      //     response.data.data.map((response) => {
      //       res2.push(response);
      //       console.log(res2);
      //     });
      //   });
      // this.jsonRoute = res2;
    },
  },
};
</script>