<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart({{ cart.length }})</div>
  <socks :premium="premium" @add-to-cart="updateCart"></socks>
</template>

<script>
import Socks from "@/components/Socks.vue";
export default {
  name: "Home",
  components: {
    Socks,
  },
  data() {
    return {
      cart: [],
      premium: true,
    };
  },
  methods: {
    updateCart(id) {
      this.cart.push(id);
    },
  },
};
</script>
