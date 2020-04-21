<template>
  <form class="review-form" @submit.prevent="addReview">
    <p>
      <label for="name">Name:</label>
      <input id="name" v-model="name" placeholder="name">
    </p>

    <p>
      <label for="review">Review:</label>
      <textarea id="review" v-model="review"></textarea>
    </p>

    <p>
      <label for="rating">Rating:</label>
      <select id="rating" v-model.number="rating">
        <option>5</option>
        <option>4</option>
        <option>3</option>
        <option>2</option>
        <option>1</option>
      </select>
    </p>

    <ul v-show="errors.length">
      <li v-for="(error, index) in errors" :key="index">{{ error }}</li>
    </ul>

    <p>
      <input type="submit" value="submit">
    </p>
  </form>
</template>

<script>
  export default {
    name: "ProductReview",
    data() {
      return {
        name: null,
        review: null,
        rating: null,
        errors: [],
      };
    },
    methods: {
      addReview() {
        this.errors = [];
        if (!this.name) this.errors.push("Name is required!");
        if (!this.rating) this.errors.push("Rating is required!");
        if (!this.review) this.errors.push("Review is required!");
        if (this.errors.length) return;

        let productReview = {
          name: this.name,
          review: this.review,
          rating: Number(this.rating),
        };

        this.$emit('review-submitted', productReview);
        this.name = null;
        this.review = null;
        this.rating = null;
      },
    },
  }
</script>

<style scoped>

</style>