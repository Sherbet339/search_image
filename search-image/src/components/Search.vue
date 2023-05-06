<template>
  <v-container class="search-component">
    <h1>Unsplash</h1>
    <v-text-field
      v-model="search"
      class="mt-6"
      append-icon="mdi-magnify"
      placeholder="Search for images"
      outlined
      hide-details
      @keyup="filter()"
    ></v-text-field>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      search: null,
    };
  },
};
</script>