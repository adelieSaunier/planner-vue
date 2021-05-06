<template>
  <nav class="main-nav">
      <router-link :to="{name: 'Home' }" >Projets</router-link>
      <router-link :to="{name: 'AddProject' }" >Nouveau projet</router-link>
  </nav>
</template>

<script>
export default {
    name:'Navbar'
}
</script>

<style scoped >
.main-nav{
    text-align: center;
    margin: 40px;
}
.main-nav a{
    display: inline-block;
    text-decoration: none;
    margin: 0 10px;
    color: #999;
    font-size: 18px;
}
a.router-link-active{
    border-bottom: 2px solid #00ce;
    padding-bottom: 4px;
}
</style>