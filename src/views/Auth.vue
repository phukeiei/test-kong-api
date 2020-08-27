<template>
  <div class="app">
    <h1>Basic-Auth</h1>
    <v-form>
      <v-text-field v-model="useranme" label="username"></v-text-field>
      <v-text-field v-model="password" label="password"></v-text-field>
      <v-btn color="warning" @click="onClick">Basic - Auth</v-btn>
    </v-form>

    <div v-if="jsonAcl">
      <hr />
      <h1>Login</h1>
      <div>
        <!-- <span :v-html="jsonAcl"></span> -->
        {{jsonAcl.config.headers.Authorization}}
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    useranme: "phurkuser1",
    password: "ivsoft",
    jsonAcl: "",
  }),

  methods: {
    async onClick() {
      let res = [];
      await axios
        .get("http://192.168.1.121/server1", {
          // Axios looks for the `auth` option, and, if it is set, formats a
          // basic auth header for you automatically.
          auth: {
            username: this.useranme,
            password: this.password,
          },
          headers: {
            "Access-Control-Allow-Origin": "*",
            Accept: "application/json",
            "Content-Type": "application/json",
          },
        })
        .then(function (response) {
          res = response;
          console.log(response);
        });
      this.jsonAcl = res;

      //

      await axios
        .get("http://192.168.1.121/server1", {
          headers: {
            Authorization: this.jsonAcl.config.headers.Authorization,
          },
        })
        .then((res) => {
          console.log("req with header success");
          console.log(res);
        })
        .catch((err) => {
          console.log("req with header error");
          console.log(err);
        });
      //
    },
  },
};
</script>