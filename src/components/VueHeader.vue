<template>
  <header>
    <div class="navbar navbar-dark bg-dark box-shadow">
      <div
        class="container-lg d-flex justify-content-between flex-grow-1 align-items-center px-5"
      >
        <a
          href="javascript:void(0)"
          class="navbar-brand d-flex align-items-center"
        >
          <img alt="Vue logo" class="img-fluid" src="../assets/logo.png" />
          <strong>{{ $t("title") }}</strong>
        </a>

        <locale class="w-10"></locale>
      </div>
    </div>
  </header>
</template>

<script>
import Locale from "./Locale";
export default {
  name: "VueHeader",
  components: { Locale },
};
</script>

<style>
header,
.container {
  height: 5rem;
}
.navbar-brand img {
  width: 10%;
}
.w-10 {
  width: 10%;
}
</style>
