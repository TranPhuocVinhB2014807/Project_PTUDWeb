<template>
    <div>
    
      <div>
        <div v-if="loggedInUser">
         <h2 class="text-center mt-3 pt-3"><b>{{ loggedInUser.username }}</b></h2>
        </div>
      
      </div>
    </div>
  </template>
  
 
  
  <style scoped>
  .page {
    text-align: left;
    max-width: 750px;
  }
  </style>
  <script>
  import { mapGetters, mapActions } from "vuex";
  export default {
    computed: {
      ...mapGetters(["loggedInUser"]),
    },
  
  };
  </script>