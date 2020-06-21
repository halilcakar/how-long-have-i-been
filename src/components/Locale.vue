<template>
  <div class="locale-changer">
    <div class="input-group">
      <select
        v-model="$root.$i18n.locale"
        class="custom-select"
        id="inputGroupSelect01"
      >
        <option v-for="(lang, i) in langs" :key="`Lang${i}`" :value="lang">{{
          lang
        }}</option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  name: "locale-changer",
  data() {
    return {
      langs: this.$i18n.availableLocales,
    };
  },
  created() {
    let userLocale = (navigator.language || navigator.userLanguage).split(
      "-"
    )[0];
    if (this.langs.includes(userLocale)) {
      this.$root.$i18n.locale = userLocale;
    }
  },
};
</script>

<style scoped>
/* select {
  border: none;
  font-weight: bold;
} */
</style>
