<template>
  <div>
    <span
      class="tab"
      :class="{ activeTab: selectedTab === index }"
      v-for="(tab, index) in tabs"
      :key="index"
      @click="selectedTab = index"
    >
      {{ tab }}
    </span>

    <div v-show="selectedTab === 0">
      <p v-if="!reviews.length">There are no reviews yet. Be the first!</p>
      <ul>
        <li v-for="(review, index) in reviews" :key="index">
          <p>{{ review.name }}</p>
          <p>Rating: {{ review.rating }}</p>
          <p>{{ review.review }}</p>
        </li>
      </ul>
    </div>

    <ProductReview v-show="selectedTab === 1">
    </ProductReview>
  </div>
</template>

<script>
  import ProductReview from "@/components/ProductReview";
  export default {
    name: "ProductTabs",
    components: {
      ProductReview,
    },
    props: {
      reviews: {
        type: Array,
        required: true,
      }
    },
    data() {
      return {
        tabs: ["Reviews", "New Review"],
        selectedTab: 0,
      };
    },
  }
</script>

<style scoped>

</style>