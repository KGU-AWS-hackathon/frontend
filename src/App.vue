<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/bike">자전거</router-link> |
    <router-link to="/kick">킥보드</router-link>
    <!-- <router-link to="/test">Test</router-link> -->
  </nav>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
nav {
  padding: 20px;
  margin-bottom: 10px;
  background-color: #f2f2f2;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  text-decoration: none;
  padding: 5px 10px;
}

nav a.router-link-exact-active {
  color: #42b983;
  background-color: #e6f4ea;
}

</style>
