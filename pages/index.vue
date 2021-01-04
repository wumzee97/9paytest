<template>
  <div>
    <v-carousel height="750" hide-delimiters cycle class="m-6 slider">
      <v-carousel-item v-for="(i, index) in sliders" :src="i" :key="index">
      </v-carousel-item>
    </v-carousel>
    <v-container>
      <v-row class="mt-16">
        <v-col md="6" cols="12">
          <h2>Merchants</h2>
        </v-col>
        <v-col md="3" cols="6">
          <v-text-field
            outlined
            dense
            v-model="searchString"
            label="Search Product"
          ></v-text-field>
        </v-col>
        <v-col md="3" cols="6">
          <v-select
            v-model="category"
            label="Sort by Category"
            outlined
            dense
            :items="['Product Merchant', 'Service Merchant']"
          >
          </v-select>
        </v-col>
      </v-row>
      <v-layout row wrap mb-8>
        <v-flex
          md3
          sm6
          xs12
          :px-8="$vuetify.breakpoint.xsOnly"
          :px-4="$vuetify.breakpoint.smAndUp"
          v-for="i in filteredProducts"
          mt-8
          :key="i.id"
        >
          <v-card
            @click=";(productDialog = true), (singleProduct = i)"
            class="product"
            flat
          >
            <div class="image-container pa-8">
              <v-img height="180" :src="i.image"></v-img>
            </div>
            <div class="pa-4 text-center">
              <h4>{{ i.name }}</h4>
            </div>
          </v-card>
        </v-flex>
        <v-flex v-if="filteredProducts.length == 0" md12 text-center>
          <img src="../static/assets/no-products-found.png" alt="" />
        </v-flex>
      </v-layout>
    </v-container>
    <v-dialog width="600" v-model="productDialog">
      <v-card class="pa-6">
        <v-layout row wrap>
          <v-flex md6 :pa-16="$vuetify.breakpoint.mdAndUp">
            <v-img height="200" :src="singleProduct.image"> </v-img>
          </v-flex>
          <v-flex md6 :py-16="$vuetify.breakpoint.mdAndUp">
            Product Name:
            <h3 class="mb-6">{{ singleProduct.name }}</h3>
            Product Category:
            <h3 class="mb-6">{{ singleProduct.category }}</h3>
            Product Price:
            <h3 class="mb-6">&#8358;{{ singleProduct.price | formatPrice }}</h3>
            <v-btn text class="primary mt-4">Buy Now</v-btn>
            <v-btn text class="secondary mt-4">Save for Later</v-btn>
          </v-flex>
        </v-layout>
      </v-card>
    </v-dialog>
  </div>
</template>
<script>
import { products } from '../util/products'
export default {
  data() {
    return {
      productDialog: false,
      searchString: '',
      category: '',
      singleProduct: [],
      products: products,
      sliders: [
        require('../static/assets/slide1.png'),
        require('../static/assets/slide2.png'),
        require('../static/assets/slide3.png'),
      ],
    }
  },
  watch: {
    category: function () {
      this.products = products
      this.selectProducts()
    },
    searchString: function () {
      this.products = products
    }
  },
  methods: {
    selectProducts() {
      var products = this.products
      var selectedProducts = []
      for (var i = 0; i < products.length; i++) {
        if (products[i].category == this.category) {
          selectedProducts.push(products[i])
        }
      }
      this.products = selectedProducts
    },
  },
  computed: {
    filteredProducts: function () {
      var products = this.products
      var searchString = this.searchString
      var category = this.category

      if (!searchString) {
        return products
      }

      searchString = searchString.trim().toLowerCase()

      products = products.filter(function (item) {
        if (item.name.toLowerCase().indexOf(searchString) !== -1) {
          return item
        }
      })
      return products
    },
  },
}
</script>
<style lang="scss" scoped>
.image-container {
  height: 250px;
  width: 100%;
  background: #333;
}
.product {
  border-radius: 0;
  &:hover {
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
      0 4px 6px -2px rgba(0, 0, 0, 0.05) !important;
  }
}

@media only screen and (max-width: 600px) {
  .slider {
    height: 300px !important;
  }
}
</style>
