<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/products">Products</router-link>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
body{
  margin:0;
  padding:0;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  // Acceptance Criteria Nr.6 - "The page should be wrapped in a centered container with a max-width of 1600px"
  max-width: 1600px;
  margin:0 auto;
 
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
