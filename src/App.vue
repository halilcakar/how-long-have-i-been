<template>
  <div id="app">
    <vue-header />

    <vue-main />

    <footer class="footer">
      <div class="container">
        <span class="text-muted"
          >Made with ❤, by
          <a href="https://github.com/halilcakar/how-long-have-i-been"
            >@halilcakar</a
          >
          Special thanks to
          <a href="https://www.linkedin.com/in/sabrina-reith-799048156/"
            >@sabrina</a
          >
          For Translation
        </span>
      </div>
    </footer>
  </div>
</template>

<script>
import VueHeader from "./components/VueHeader";
import VueMain from "./components/VueMain";

export default {
  name: "App",
  components: {
    VueHeader,
    VueMain,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
html {
  position: relative;
  min-height: 100%;
}
body {
  margin-bottom: 60px; /* Margin bottom by footer height */
}
.footer {
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 5rem; /* Set the fixed height of the footer here */
  line-height: 5rem; /* Vertically center the text there */
  background-color: #f5f5f5;
}
.container {
  width: auto;
  max-width: 680px;
  padding: 0 15px;
}
</style>
