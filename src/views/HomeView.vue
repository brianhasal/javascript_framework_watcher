<script>
import axios from 'axios';

  export default {
    data: function () {
      return {
        apis: []

      };
    },
    created: function () {
      this.indexApis();
    },
    methods: {
      indexApis: function () {
        axios.get("/api.json").then((response) => {
          console.log("Retrieving APIs", response);
          this.apis = response.data;
        })
      }
    
    },
  };
</script>



<template>
  <div class="home">
    <h1>LIST OF APIS</h1>
    <p>{{this.apis}}</p>
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