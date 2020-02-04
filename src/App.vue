<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style>
body {
  font-family: "Noto Sans", sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
}

#nav {
}

a {
}

a.router-link-exact-active {
  color: #1a73e8;
  text-decoration: none;
  font-size: 14px;
  position: relative;
}
a.router-link-exact-active::after {
  content: "";
  position: absolute;
}
</style>
