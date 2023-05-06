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

    <h4 v-if="noImage === true">
      No images found from this keyword "{{ this.search }}"
    </h4>
    <v-row class="mt-6">
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
    <div class="load-btn mt-5">
      <v-btn
        v-if="displayAmount < allImage.length && noImage === false"
        @click="loadMore()"
      >
        Load more
      </v-btn>
    </div>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      search: null,
      allImage: [],
      images: [],
      dialog: false,
      displayAmount: null,
      noImage: false,
    };
  },
  mounted() {},
  methods: {
    searchImage() {
      this.displayAmount = 8;
      this.images = [];
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
          if (data.total < 1) {
            this.noImage = true;
          } else {
            this.noImage = false;
            this.allImage = data.results;
            for (let i = 0; i < this.displayAmount; i++) {
              this.images.push({
                selected: false,
                image: data.results[i].urls.regular,
              });
            }
            console.log(this.images);
          }
        });
    },
    loadMore() {
      this.images = [];
      this.displayAmount += 4;
      console.log(this.allImage);

      for (let i = 0; i < this.displayAmount && i < this.allImage.length; i++) {
        this.images.push({
          selected: false,
          image: this.allImage[i].urls.regular,
        });
      }
      console.log(this.images);
    },
  },
};
</script>