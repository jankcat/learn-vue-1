<template>
  <div id="app">
    <div class="cart">
      <p>Cart({{ cart.length }})</p>
    </div>
    <Learn pic="cat1.png" :premium="premium" @add-to-cart="updateCart"/>
  </div>
</template>

<script>
import Learn from './components/Learn';

export default {
  name: 'App',
  components: {
    Learn
  },
  data () {
    return {
      premium: true,
      cart: [],
    };
  },
  methods: {
    updateCart(id) {
      this.cart.push(id);
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
