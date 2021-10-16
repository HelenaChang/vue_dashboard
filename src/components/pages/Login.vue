<template>
    <div class="text-center">
        <form class="form-signin" @submit.prevent="signin">
        <a href="index.html"><img class="mb-3" src="../../assets/images/SweetHeart_logo.svg" alt="SweetHeart" width="250" height="100">
        </a>
        
        <h1 class="h3 mb-3 font-weight-normal text-secondary">Please sign in</h1>
        <label for="inputEmail" class="sr-only">Email address</label>
        <input type="email" id="inputEmail" class="form-control" v-model="user.username" placeholder="Email address" required autofocus>
        <label for="inputPassword" class="sr-only">Password</label>
        <input type="password" id="inputPassword" class="form-control" v-model="user.password" placeholder="Password" required>
        <div class="checkbox mb-3 text-left">
            <label>
                <input type="checkbox" value="remember-me"> Remember me
            </label>
        </div>
        <button class="btn btn-lg btn-primary btn-block text-white" type="submit">Sign in</button>
        <p class="mt-5 mb-3 text-muted">&copy; 僅供練習 無任何商業用途</p>
    </form>
    </div>
</template>

<script>
export default {
 
  data() {
    return {
      user: {
        username: '',
        password: '',
      },
    };
  },
  methods: {
    signin() {
      const api = `${process.env.APIPATH}/admin/signin`;
      const vm = this;
      this.$http.post(api, vm.user).then((response) => {
        if (response.data.success) {
          const token = response.data.token;
          const expired = response.data.expired;
          document.cookie = `sweetToken=${token};expires=${new Date(expired)};`;
          vm.$router.push('/admin/products');
        }
      });
    },
  },
  
};

</script>

<style scoped>
  .form-signin {
  width: 100%;
  max-width: 330px;
  padding: 15px;
  margin: 0 auto;
}
.form-signin .checkbox {
  font-weight: 400;
}
.form-signin .form-control {
  position: relative;
  box-sizing: border-box;
  height: auto;
  padding: 10px;
  font-size: 16px;
}
.form-signin .form-control:focus {
  z-index: 2;
}
.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}


</style>