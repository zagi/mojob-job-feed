<template>
  <v-app id="app">
    <v-container>
      <router-view />

      <div id="nav">
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link>
      </div>
    </v-container>
  </v-app>
</template>

<style>
#app {
  font-family: Avenir, Muli, sans-serif !important;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
}
#nav {
  padding: 30px;
  text-align: center;
}
#nav a {
  font-weight: bold;
  color: #4f4f4f;
}
#nav a.router-link-exact-active {
  color: #46bbb3;
}
</style>
