<template>
  <v-container :fluid="true" class="py-0">
    <v-row class="text-center">
      <!--  header background -->
      <v-col cols="12" class="px-0 py-0">
        <v-img
          :src="require('../assets/background/10.jpg')"
          class="mb-3 p"
          cover
          height="300"
        />
      </v-col>
      <!--header background -->

      <!-- Keyword Form Section -->

      <v-col cols="9" class="mx-auto">
        <section class="product-form-section style-two">
          <div class="auto-container">
            <div class="inner-container margin-top">
              <!-- Default Form -->
              <div class="default-form">
                <form>
                  <v-row>
                    <v-col class="col">
                      <v-text-field
                        v-model="keyword"
                        label="keyword"
                        v-on:input="searchForRecepie()"
                      ></v-text-field>
                    </v-col>
                    <v-col class="col-md-4 col-12">
                      <v-select
                        :items="filters"
                        :menu-props="{ maxHeight: '400' }"
                        v-model="selectedFilters"
                        label="Filtres"
                        multiple
                        v-on:change="searchForRecepie"
                        persistent-hint
                      ></v-select>
                    </v-col>
                  </v-row>
                </form>
              </div>
            </div>
          </div>
        </section>
      </v-col>
      <!-- End Keyword Form Section -->
    </v-row>

    <v-row>
      <v-col cols="12" class="px-0">
        <section class="popular-recipes-section">
          <v-row class="px-md-3">
            <v-col class="col-md-9 col-12 mx-auto">
              <v-row>
                <v-col
                  class="col-md-4 col-12 px-md-0 px-4"
                  v-for="item in recepies"
                  :key="item.label"
                >
                  <RecepieItem :item="item"></RecepieItem>
                </v-col>
              </v-row>
            </v-col>
          </v-row>
        </section>
      </v-col>

      <v-col cols="12"> </v-col>
    </v-row>
  </v-container>
</template>

<script>
import RecepieItem from "./RecepieItem";
import axios from "axios";
export default {
  name: "HelloWorld",

  containerFluid: true,
  components: {
    RecepieItem: RecepieItem,
  },
  data: () => ({
    keyword: "",
    selectedFilters: [],
    filters: ["sans alcool", "sans gluten"],
    appId: "e8681759",
    appKey: "ec76b17c3414a24c3e549fcdb731c2b3",
    url: "https://api.edamam.com/search",
    recepies: [],
  }),
  mounted() {
    //searching for recepies on init
    this.searchForRecepie();
  },

  methods: {
    searchForRecepie() {
      let url = this.url + "?app_id=" + this.appId + "&app_key=" + this.appKey;
      let query = this.keyword.length ? "&q=" + this.keyword : "&q=" + "pizza";

      this.selectedFilters.includes("sans alcool")
        ? (query += "&health=alcohol-free")
        : "";
      this.selectedFilters.includes("sans gluten")
        ? (query += "&health=gluten-free")
        : "";

      // I Have added a set time out to avoid Throttling calls
      setTimeout(() => {
        axios.get(url + query).then((d) => {
          this.recepies = d.data.hits;
        });
      }, 1000);
    },
  },
};
</script>
<style  scoped>
.product-form-section {
  position: relative;
}
.product-form-section .inner-container.margin-top {
  margin-top: -85px;
}

@media (max-width: 500px) {
  .product-form-section .inner-container.margin-top {
    margin-top: -185px;
  }
}

.product-form-section .inner-container {
  position: relative;
  padding: 3px 20px 5px;
  border-radius: 8px;
  z-index: 1;
  background-color: #ffffff;
  box-shadow: 0px 10px 15px rgba(0, 0, 0, 0.06);
}

.popular-recipes-section {
  position: relative;
  overflow: hidden;
  padding: 90px 0px 60px;
  background: #faf3f1 url(../assets/background/1.png);
  background-size: cover;
  margin-top: -75px;
  min-height: 100vh;
}
</style>