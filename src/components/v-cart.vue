<template>
  <div class="v-cart">
    <router-link :to="{ name: 'catalog' }">
      <div class="v-cart__back">Back to catalog</div>
    </router-link>

    <h1>Cart</h1>

    <div v-if="CART.length" class="v-cart__list">
      <v-cart-item
          v-for="(item, index) in CART"
          :key="item.article"
          :cart_item_data="item"
          @deleteFromCart="deleteFromCart(index)"
      />
    </div>

    <p v-else>There are no products in cart!</p>

  </div>
</template>

<script>
import vCartItem from '@/components/v-cart-item';
import { mapActions, mapGetters } from "vuex";

export default {
  name: "v-cart",
  components: {
    vCartItem,
  },
  methods: {
    ...mapActions([
      'DELETE_FROM_CART'
    ]),
    deleteFromCart(index) {
      this.DELETE_FROM_CART(index);
    },
  },
  computed: {
    ...mapGetters([
      'CART'
    ]),
  },
}
</script>

<style lang="scss">
  .v-cart__back {
    position: absolute;
    top: 10px;
    right: 10px;
    padding: $padding * 2;
    border: 1px solid #aeaeae;
  }
</style>
