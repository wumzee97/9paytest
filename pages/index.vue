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
export default {
  data() {
    return {
      productDialog: false,
      searchString: '',
      category: '',
      singleProduct: [],
      sliders: [
        require('../static/assets/slide1.png'),
        require('../static/assets/slide2.png'),
        require('../static/assets/slide3.png'),
      ],
      products: [
        {
          id: 1,
          name: 'Mama Gold Rice',
          image: require('../static/assets/rice.jpg'),
          category: 'Product Merchant',
          price: 23000,
        },
        {
          id: 2,
          name: 'Wrist Watch',
          image: require('../static/assets/wristwatch.jpg'),
          category: 'Service Merchant',
          price: 10000,
        },
        {
          id: 3,
          name: 'Wachine Machine',
          image: require('../static/assets/washing machine.jpg'),
          category: 'Product Merchant',
          price: 60000,
        },
        {
          id: 4,
          name: 'Gas Cooker',
          image: require('../static/assets/gas cooker.jpg'),
          category: 'Service Merchant',
          price: 30000,
        },
        {
          id: 5,
          name: 'Vinegar Sellamin',
          image: require('../static/assets/vinegar.jpg'),
          category: 'Product Merchant',
        },
        {
          id: 6,
          name: 'Thermacool Refrigerator',
          image: require('../static/assets/refrigerator.jpg'),
          category: 'Product Merchant',
          price: 150000,
        },
        {
          id: 7,
          name: 'Maggi Chicken',
          image: require('../static/assets/maggi.jpg'),
          category: 'Service Merchant',
          price: 2000,
        },
        {
          id: 8,
          name: 'Milo Beverage',
          image: require('../static/assets/milo.jpg'),
          price: 1500,
        },
        {
          id: 9,
          name: 'Phillips Pressing Iron',
          image: require('../static/assets/iron.jpg'),
          category: 'Product Merchant',
        },
        {
          id: 10,
          name: 'Electric Kettle',
          image: require('../static/assets/kettle.jpg'),
          category: 'Product Merchant',
          price: 7000,
        },
        {
          id: 11,
          name: 'HP Printer',
          image: require('../static/assets/printer.png'),
          price: 40000,
        },
        {
          id: 12,
          name: 'Fitted Shirt',
          image: require('../static/assets/shirt.png'),
          category: 'Product Merchant',
          price: 6000,
        },
        {
          id: 13,
          name: 'Toasting Machine',
          image: require('../static/assets/toaster.jpg'),
          category: 'Service Merchant',
          price: 23000,
        },
        {
          id: 14,
          name: 'Brazillian Wig',
          image: require('../static/assets/wig.jpg'),
          category: 'Service Merchant',
          price: 90000,
        },
        {
          id: 15,
          name: 'PS4 Game',
          image: require('../static/assets/ps4.jpg'),
          category: 'Product Merchant',
          price: 560000,
        },
        {
          id: 16,
          name: 'Barbie Doll',
          image: require('../static/assets/doll.jpg'),
          price: 4000,
        },
        {
          id: 17,
          name: 'Fotomi',
          image: require('../static/assets/fotomi.jpg'),
          category: 'Product Merchant',
          price: 40000,
        },
        {
          id: 18,
          name: 'Golden Morn',
          image: require('../static/assets/golden morn.jpg'),
          category: 'Service Merchant',
          price: 2000,
        },
        {
          id: 19,
          name: 'iPhone',
          image: require('../static/assets/iphone.png'),
          category: 'Service Merchant',
          price: 360000,
        },
        {
          id: 20,
          name: 'Bluetooth Speaker',
          image: require('../static/assets/Bluetooth Speaker.jpg'),
          category: 'Service Merchant',
          price: 14000,
        },
      ],
    }
  },
  watch: {
    category: function () {
      var products = this.products
      products = products.filter(function (item) {
        if (item.category.toLowerCase().indexOf(this.category) !== -1) {
          return item
        }
      })
    },
  },
  computed: {
    filteredProducts: function () {
      var products = this.products
      var searchString = this.searchString

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
