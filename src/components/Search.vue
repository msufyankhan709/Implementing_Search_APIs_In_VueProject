<template>
    <div>
      <h2>Top Trending Searches</h2>
      <ul>
        <li v-for="trend in topTrends" :key="trend">{{ trend }}</li>
      </ul>
  
      <h2>Perform Search</h2>
      <input v-model="searchQuery" placeholder="Enter your search query" />
      <button @click="performSearch">Search</button>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'SearchApp',
    data() {
      return {
        topTrends: [],
        searchQuery: "",
      };
    },
    mounted() {
      this.getTopTrends();
    },
    methods: {
      getTopTrends() {
        axios.get("http://localhost:8080/api/search/top").then((response) => {
          this.topTrends = response.data;
        });
      },
      performSearch() {
        axios
          .post("http://localhost:8080/api/search/5", { query: this.searchQuery, device: "Web Browser" })
          .then(() => {
            console.log("Search performed successfully");
            // Optionally, update the top trends after performing a search
            this.getTopTrends();
          })
          .catch((error) => {
            console.error("Error performing search", error);
          });
      },
    },
  };
  </script>
  
  <style scoped>
  /* Add your component styles here */
  </style>
  