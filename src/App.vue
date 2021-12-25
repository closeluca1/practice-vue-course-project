<template>
  <Navbar :logo="logo_src" :alt="app_name" />
  <router-view />
  
  <Footer />
</template>

<script>
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";
export default {
  components: {
    Navbar,
    Footer,
  },
  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Monte seu Hamburger",
    };
  },
};
</script>

<style>

    *{
        margin: 0;
        padding: 0;
        font-family: Arial, Helvetica, sans-serif;
    }
    main{
        min-height: 50vw;
    }
    .main-container{
        min-height: 250px;
        margin: 50px;
    }
    h1{
        text-align: center;
        text-transform: uppercase;
        font-size: 42px;
        margin-bottom: 30px;
        color: #222;
    }
</style>
