<template>
    <div>
    
      <div>
        <div v-if="loggedInUser">
         <h2 class="text-center mt-3 pt-3"><b>Chào mừng <span class="text-primary">{{ loggedInUser.username }}</span> đến với trang quản trị!!</b></h2>
        </div>
        <div class="text-center">
          <img src="https://img5.thuthuatphanmem.vn/uploads/2022/01/12/hinh-nen-powerpoint-chao-mung-bai-giang_015414262.jpg" alt="" width="60%" class="">
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