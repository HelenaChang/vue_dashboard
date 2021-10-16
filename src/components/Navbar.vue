<template>
    <div>
        <nav class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0 m-0 shadow">
            <a class="navbar-brand col-md-3 col-lg-2 m-0 px-3" href="#">Sweet Heart 恬心烘焙</a>
            <button class="navbar-toggler position-absolute d-md-none collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#sidebarMenu" aria-controls="sidebarMenu" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <input class="form-control form-control-dark w-100" type="text" placeholder="Search" aria-label="Search">
            <ul class="navbar-nav bg-light ml-2 p-3">
                <li class="nav-item text-nowrap">
                <a class="nav-info" href="#" @click.prevent="signout">Sign out</a>
                </li>
            </ul>
        </nav>
    </div>
</template>

<script>
export default {
  name: 'Navbar',
  data() {
    return {
      
    }
  },
  methods: {
    signout() {
      const vm = this;
      const url = `${process.env.APIPATH}/logout`;
      this.$http.post(url).then((response) =>{
        if(response.data.success) {
          vm.$router.push('/');
        };
      });
    },
  },
}
</script>