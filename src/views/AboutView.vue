<script>
import axios from "axios";

export default {
  data: function () {
    return {
      profile: {},
    };
  },
  created: function () {
    var githubAccessToken = localStorage.getItem("github_access_token");
    if (githubAccessToken) {
      console.log(githubAccessToken);
      axios.get("/github_profile?github_access_token=" + githubAccessToken).then((response) => {
        console.log(response.data);
        this.profile = response.data;
      });
    }
  },
};
</script>

<template>
  <div class="about">
    <h1>GitHub profile!</h1>
    <h2>{{ profile.name }}</h2>
    <img v-bind:src="profile.avatar_url" alt="" />
  </div>
</template>
