<template>
  <!-- Section: Design Block -->
  <section class="">
    <!-- Jumbotron -->
    <div class="px-4 py-5 px-md-5 text-center text-lg-start">
      <div class="container">
        <div class="row gx-lg-5 align-items-center justify-content-center">
          <div class="col-lg-12 mb-2 mb-lg-0">
            <h1 class="my-4  fw-bold ls-tight">
              <span>Trang quản trị</span>
            </h1>

          </div>

          <div class="col-lg-6 mb-5 mb-lg-0">
            <div class="card">
              <div class="card-body py-5 px-md-5">
                <form @submit.prevent="login">
                    <h4 class="text-center"> Đăng nhập</h4>
                  <div data-mdb-input-init class="form-outline mb-4">
                    <input type="text" id="form3Example3" class="form-control" v-model="nhanvien.username" placeholder="Họ tên nhân viên" />
                  </div>


                  <div data-mdb-input-init class="form-outline mb-4">
                    <input type="password" id="form3Example4" class="form-control" v-model="nhanvien.password"  placeholder="Password"/>
                  </div>


                  <button type="submit" data-mdb-button-init data-mdb-ripple-init
                    class="btn btn-primary btn-block mb-4">
                    Đăng nhập
                  </button>
                  <p v-if="error">{{ error }}</p>


                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

  </section>

</template>
<script>
import { mapActions } from 'vuex';
import nhanvienService from "@/services/nhanvien.service"

export default {
  data() {
    return {
      nhanvien: { username: '', password: '' },
      error: '',
    };
  },
  methods: {
    ...mapActions(['setLoggedInUser']),
    async login() {
      try {
        const response = await nhanvienService.login(this.nhanvien);
        if (response.status === "success") {
          console.log('response:', response);

          localStorage.setItem('loggedInUser', JSON.stringify({ username: response.user.HOTENNV, id: response.user._id ,role:"admin"}));
          this.setLoggedInUser({ username: response.user.HOTENNV, id: response.user._id, role: "admin" });
      //  console.log('loggedInUser:',loggedInUser.role);
          
          this.$router.push('/quanly');
        } else {
          this.error = 'Tên đăng nhập hoặc mật khẩu không chính xác.';
        }
      } catch (error) {
        this.error = 'Đăng nhập không thành công. Vui lòng thử lại.';
      }
    }
  },
  created() {
    // Kiểm tra nếu có thông tin đăng nhập trong local storage khi component được tạo
    const loggedInUser = localStorage.getItem('loggedInUser');
    if (loggedInUser) {
      this.$store.dispatch('setLoggedInUser', JSON.parse(loggedInUser));
    }
  }
};
</script>
