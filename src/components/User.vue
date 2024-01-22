<template>
    <div>
      <h2>User Registration</h2>
      <input v-model="username" placeholder="Enter your username" />
      <button @click="registerUser">Register</button>
  
      <h2>Add User Data</h2>
      <input v-model="userData" placeholder="Enter additional user data" />
      <button @click="addUserData">Add User Data</button>

      <button @click="deleteUserData">Delete User Data</button>


      <ul>
        <li v-for="user in addUser" :key="user">{{ user.device }}</li>
      </ul>
    </div>
  </template>
  
  <script>
import axios from 'axios';

  export default {
    name:'UserApp',
    data() {
      return {
        username: "",
        userData: "",
        userId : 5,
        deviceId: "Web Browser",
        addUser:{}
      };
    },
    mounted() {
      this.getUser();
    },
    methods: {
      registerUser() {
        // Make API request to register a new user
        // You need to replace the URL with your actual Spring Boot API endpoint
        axios
          .post("http://localhost:8080/api/add/user", { userId: this.userId, deviceId: this.deviceId })
          .then((response) => {
            console.log("User registered successfully", response.data);
          })
          .catch((error) => {
            console.error("Error registering user", error);
          });
      },
      getUser(){
        axios.get("http://localhost:8080/api/search/1").then((response) => {
          this.addUser = response.data;
          console.log("Data is showing");
        });
      },
      addUserData() {
        // Make API request to add user data
        // You need to replace the URL with your actual Spring Boot API endpoint
        axios
          .post("http://localhost:8080/api/user/1", { searchData: this.userData })
          .then((response) => {
            console.log("User data added successfully", response.data);
          })
          .catch((error) => {
            console.error("Error adding user data", error);
          });
      },
      deleteUserData() {
      const userId = 5; // Replace with the actual user ID you want to delete

      // Make a DELETE request to your backend API
      axios
        .delete(`http://localhost:8080/api/search/${userId}`)
        .then((response) => {
          // Check if the request was successful
          if (response.status === 200) {
            console.log('User data deleted successfully');
            // Optionally, you can update your component state or perform other actions
          } else {
            console.error('Error deleting user data');
          }
        })
        .catch((error) => {
          console.error('Error deleting user data', error);
          // Handle errors, show a message, or perform other actions as needed
        });
    },
    },
  };
  </script>
  
  <style scoped>
  /* Add your component styles here */
  </style>
  