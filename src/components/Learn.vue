<template>
  <div class="product">
    <div class="product-image">
      <img :src="image"/>
    </div>

    <div class="product-info">
      <h1>{{ name }}</h1>
      <p>{{ description }}</p>
      <p>Shipping: {{ shipping }}</p>
      <p v-if="qty > 10">In Stock</p>
      <p v-else-if="qty <= 10 && qty > 0">Almost Sold Out!</p>
      <p v-else>Out of Stock</p>

      <ul>
        <li v-for="detail in details" :key="detail">{{ detail }}</li>
      </ul>

      <div
        v-for="(variant, index) in variants"
        :key="variant.id"
        class="color-box"
        :style="{ backgroundColor: variant.color }"
        @mouseover="updateProduct(index)"
      >
      </div>

      <button
        v-on:click="addToCart"
        :disabled="!qty"
        :class="{ disabledButton: !qty }"
      >
        Add to cart
      </button>

      <ProductTabs :reviews="reviews"></ProductTabs>

    </div>
  </div>
</template>

<script>
  import ProductTabs from "@/components/ProductTabs";

  export default {
    name: "Learn",
    components: {
      ProductTabs,
    },
    props: {
      pic: {
        type: String,
        required: true,
      },
      premium: {
        type: Boolean,
        required: true,
      },
    },
    data() {
      return {
        product: "Cat",
        brand: "Kitten Inc.",
        description: "fuzzy wuzzy",
        selectedVariant: 0,
        details: [
          "Fuzzy",
          "Cuddly and cute",
          "Lots of whiskers",
        ],
        variants: [
          {
            id: 1,
            color: 'green',
            image: "cat1.png",
            qty: 10,
          },
          {
            id: 2,
            color: 'blue',
            image: 'cat2.jpeg',
            qty: 0,
          },
        ],
        reviews: [],
      };
    },
    computed: {
      name() {
        return `${this.brand} ${this.product}`;
      },
      image() {
        return this.variants[this.selectedVariant].image;
      },
      qty() {
        return this.variants[this.selectedVariant].qty;
      },
      shipping() {
        return this.premium ? "Free!" : 2.99;
      }
    },
    methods: {
      updateProduct(index) {
        this.selectedVariant = index;
      },
      addToCart() {
        this.$emit('add-to-cart', this.variants[this.selectedVariant].id);
      },
      addReview(review) {
        this.reviews.push(review);
      },
    },
  };
</script>

<style scoped>

</style>