<template>
  <v-container :fluid="true" class="pt-0">
    <div class="inner-box">
      <div class="image">
        <a href="recipes-detail.html"
          ><img :src="item.recipe.image" alt=""
        /></a>
      </div>
      <div class="lower-content">
        <v-dialog v-model="dialog" width="500">
          <template v-slot:activator="{ on, attrs }">
            <h4 v-bind="attrs" v-on="on">{{ item.recipe.label }}</h4>
          </template>

          <v-card>
            <v-card-title class="headline">
              {{ item.recipe.label }}
            </v-card-title>

            <v-card-text>
              <v-row>
                <v-col class="section-title">
                  Source : {{ item.recipe.source }}
                </v-col>
              </v-row>
              <v-row>
                <v-col class="section-title"> Ingredients : </v-col>
              </v-row>
              <v-row>
                <v-col
                  class="py-0 col-md-6 col-12"
                  v-for="(ing,i) in item.recipe.ingredients"
                  :key="ing.text+i"
                >
                  {{ ing.text }}
                </v-col>
              </v-row>
              <v-row>
                <v-col class="section-title"> Valeur nutritionnelle : </v-col>
              </v-row>
              <v-row>
                <v-col
                  cols="6"
                  class="py-0"
                  v-for="(nut,index) in item.recipe.digest"
                  :key="nut.label+index"
                >
                  {{ nut.label }} {{ nut.total.toFixed() }} {{ nut.unit }}
                </v-col>
              </v-row>
            </v-card-text>

            <v-divider></v-divider>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="primary" text @click="dialog = false">
                Fermer
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </div>
    </div>
  </v-container>
</template>

<script>
export default {
  name: "RecepieItem",
  props: ["item"],

  data: () => ({
    dialog: false,
  }),
};
</script>
<style  scoped>
.inner-box .lower-content {
  background-color: #ffffff;
  padding: 15px 20px;
  min-height: 80px;
  text-align: left;
}
h4:hover {
  color: #ff7d5f;
  cursor: pointer;
}
.inner-box .image {
  position: relative;
  overflow: hidden;
  background-color: #262626;
}

.inner-box .image img {
  position: relative;
  width: 100%;
  height: 230px;

  display: block;
  object-fit: cover;
  -webkit-transition: all 600ms ease;
  -ms-transition: all 600ms ease;
  -o-transition: all 600ms ease;
  -moz-transition: all 600ms ease;
  transition: all 600ms ease;
}
.inner-box:hover .image img {
  opacity: 0.5;
  transform: scale(1.07, 1.07);
}
.section-title {
  position: relative;
  color: #ff7d5f;
  font-size: 14px;
  letter-spacing: 1px;
  padding: 6px 18px;
  display: inline-block;
  text-transform: uppercase;
  /* background-color: #ffffff; */
  font-weight: 500;
}
</style>