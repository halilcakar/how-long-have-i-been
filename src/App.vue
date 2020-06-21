<template>
  <div id="app">
    <div id="logo">
      <img
        width="120rem"
        height="120rem"
        alt="Vue logo"
        src="./assets/logo.png"
      />
      <locale></locale>
    </div>
    <calculator />
  </div>
</template>

<script>
import Calculator from "./components/Calculator";
import Locale from "./components/Locale";

export default {
  name: "App",
  components: {
    Calculator,
    Locale,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#logo {
  display: flex;
  justify-content: center;
}
</style>
