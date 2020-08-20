<template>
  <v-card>
    <v-card-title>
      Nutrition
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>
    <v-data-table :headers="headers" :items="consumers" :search="search">
      
    </v-data-table>
  </v-card>
</template>

<script>
import axios from "axios";
export default {
  async mounted() {
    let res = [];
    await axios
      .get("http://localhost:8001/consumers")
      .then(function (response) {
        response.data.data.map((response) => {
          if (!response.custom_id) {
            response.custom_id = "-";
          }
          res.push(response);
          console.log(res);
        });
      });
    this.consumers = res;
  },
  data() {
    return {
      search: "",
      headers: [
        {
          text: "Custom Id",
          value: "custom_id",
          align: "start",
          sortable: false,
        },
        { text: "Created At", value: "created_at" },
        { text: "Id", value: "id" },
        { text: "Username", value: "username" },
      ],
      consumers: [],
    };
  },
};
</script>
