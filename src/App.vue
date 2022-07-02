<template>
  <nav>
    <router-link to="/">Início</router-link>
    <router-link to="/archive">Arquivo</router-link>
    <!-- <router-link to="/about">Sobre</router-link> -->
  </nav>
  <router-view />
</template>

<style>
body {
  background: #edf0f5;
}

#app {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 80%;
  margin: 50px auto;
}

nav {
  color: rgb(167, 167, 167);
  width: 80%;
  margin: 0 auto;
  text-align: center;
}

h1 {
  text-align: center;
  font-weight: 900;
  font-size: 2rem;
  margin: 3rem 0 2rem 0;
}

nav a {
  color: #1643B6;
  font-weight: bold;
  margin: 0 1rem 0 0;
  border-radius: 14px;
  text-decoration: none;
  padding: 0.25rem 0.75rem;
}

input[type="text"] {
  width: 80%;
}

input[type="submit"] {
  background: #1643b6;
  color: white;
  border-radius: 10px;
  padding: 1rem 1rem;
  border: none;
  box-shadow: 0 5px 10px #8aa4e5;
  font-size: 1rem;
  font-weight: 300;
  transition: all 0.25s ease-out;
  cursor: pointer;
  margin-left: 2.5% !important;
}
input[type="checkbox"] {
  width: auto;
  margin: 0 0.8rem 0 0;
}
input[type="submit"]:hover {
  background: #1a44a5;
  box-shadow: 0 3px 7px #357fcf;
}
input {
  border-radius: 10px;
  box-sizing: border-box;
  border: 1px solid #aaa;
  font-size: 1rem;
  padding: 0.8rem 1rem;
}
</style>

<script>
import { useStore } from "vuex";

export default {
  beforeCreate() {
    const store = useStore();
    store.commit("loadStore");
  },
};
</script>
