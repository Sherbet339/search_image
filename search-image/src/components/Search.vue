<template>
  <v-container class="search-component">
    <h1>Unsplash</h1>
    <v-row justify="center">
      <v-col md="7">
        <v-text-field
          v-model="search"
          class="mt-6"
          append-icon="mdi-magnify"
          placeholder="Search for images"
          outlined
          hide-details
          @keyup.enter="searchImage()"
        ></v-text-field>
      </v-col>
    </v-row>

    <v-row class="text-center mt-6">
      <v-col md="3" sm="3" xs="2" v-for="(img, index) in images" :key="index">
        <v-dialog class="img-dialog" v-model="img.selected" width="auto">
          <template v-slot:activator="{ on, attrs }">
            <v-img
              :src="img.image"
              max-width="400"
              max-height="300"
              v-bind="attrs"
              v-on="on"
            ></v-img>
          </template>
          <v-card class="img-expand pa-5">
            <div class="close-btn">
              <v-icon @click="img.selected = false">mdi-close </v-icon>
            </div>
            <v-img :src="img.image" max-width="400" max-height="400"></v-img>
          </v-card>
        </v-dialog>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      search: null,
      images: [],
      dialog: false,
    };
  },
  mounted() {},
  methods: {
    searchImage() {
      console.log(this.search);
      let clientId = "wqLsrKsFmjHksm5ixxQdKmgyHrXuHfVtFL_AGxAuY1c";
      let url =
        "https://api.unsplash.com/search/photos/?client_id=" +
        clientId +
        "&query=" +
        this.search;

      fetch(url)
        .then((res) => {
          return res.json();
        })
        .then((data) => {
          console.log(data.results);
          data.results.forEach((image) => {
            this.images.push({ selected: false, image: image.urls.regular });
          });
          console.log(this.images);
        });
    },
  },
};
</script>