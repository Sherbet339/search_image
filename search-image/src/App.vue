<template>
  <v-app>
    <v-main>
      <Search />
    </v-main>
  </v-app>
</template>

<script>
import Search from "./components/Search.vue";

export default {
  name: "App",

  components: {
    Search,
  },

  data() {
    return {}
  },
};
</script>

<style lang="scss">
@import "@/assets/scss/_global.scss";
</style>