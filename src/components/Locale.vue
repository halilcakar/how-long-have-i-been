<template>
  <div class="locale-changer">
    <select v-model="$root.$i18n.locale">
      <option v-for="(lang, i) in langs" :key="`Lang${i}`" :value="lang">{{
        lang
      }}</option>
    </select>
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
};
</script>

<style scoped>
select {
  border: none;
  font-weight: bold;
}
</style>
