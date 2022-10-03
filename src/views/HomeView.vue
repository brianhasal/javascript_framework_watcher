<script>
import axios from "axios";

export default {
  data: function () {
    return {
      apis: [],
    };
  },
  created: function () {
    var code = this.$route.query.code;
    if (code) {
      axios.get("/auth/github/callback?code=" + code).then((response) => {
        console.log(response.data);
        localStorage.setItem("github_access_token", response.data.access_token);
        this.$router.push("/about");
      });
    }

// http://localhost:3000/auth/github/callback?code=6fa712b2514f95dbdc31

    this.indexApis();
  },
  methods: {
    indexApis: function () {
      // axios
      //   .all([
      //     axios.get("https://api.github.com/vuejs/vue"), 
      //     axios.get("https://api.github.com/angular/angular.js"),
      //     axios.get("https://api.github.com/emberjs/ember.js"),
      //     axios.get("https://api.github.com/sveltejs/svelte"),
      //     axios.get("https://api.github.com/facebook/react")
      //     ])
      //   .then(
      //     axios.spread(function (response1, response2, response3, response4, response5) {
      //       this.apis << response1,
      //       this.apis << response2,
      //       this.apis << response3,
      //       this.apis << response4,
      //       this.apis << response5
      //     })
      //   );

      axios.get("/api").then((response) => {
        console.log("Retrieving APIs", response);
        this.apis = response.data;
      })
    },

    // updateApis: function () {
    //   axios.post()
    // }
  },
};
</script>

<template>
  <div class="home">
    <h1>LIST OF APIS</h1>
    <a href="https://github.com/login/oauth/authorize?client_id=0b609ab45aba0e6acc84">
      Log in with Github ID
    </a>
    <p>{{ this.apis }}</p>

    <div v-for="api in apis" :key="api.id">
      <h3>
        {{api.stars}} Stars
        {{api.watchers}} Watchers
        {{api.forks}} Forks
      </h3>
    </div>

  </div>
</template>

<style></style>
