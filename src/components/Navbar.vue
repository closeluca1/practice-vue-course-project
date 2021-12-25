<template>
  <div id="nav">
    <router-link to="/" id="logoUrl">
      <img :src="logo" :alt="alt" id="logo" />
    </router-link>

    <router-link to="/">Home</router-link>

    <router-link to="/orders">Pedidos</router-link>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  props: ["logo", "alt"],
};
</script>

<style scoped>
#nav {
  padding: 15px 50px;
  display: flex;
  align-content: center;
  justify-content: flex-end;
  border-bottom: 4px solid #111;
  background: #222;
}
#nav #logoUrl {
  margin: auto;
  margin-left: 0;
}
#logo {
    width: 40px;
}
#nav a{
    margin: 12px;
    text-decoration: none;
    color: #fcba03;
    transition: .3s;
}
#nav a:hover{
    color: #fafafa;
}
</style>
