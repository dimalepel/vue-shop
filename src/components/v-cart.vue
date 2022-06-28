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
          @decrement="decrement(index)"
          @increment="increment(index)"
      />
      <div class="v-cart__total">
        <p class="total__name">Total:</p>
        <p>{{ cartTotalCost }} $</p>
      </div>
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
      'DELETE_FROM_CART',
      'DECREMENT_CART_ITEM',
      'INCREMENT_CART_ITEM',
    ]),
    decrement(index) {
      this.DECREMENT_CART_ITEM(index);
    },
    increment(index) {
      this.INCREMENT_CART_ITEM(index);
    },
    deleteFromCart(index) {
      this.DELETE_FROM_CART(index);
    },
  },
  computed: {
    ...mapGetters([
      'CART'
    ]),
    cartTotalCost() {
      let result = [];

      if (this.CART.length) {
        for (let item of this.CART) {
          result.push(item.price * item.quantity);
        }

        result = result.reduce(function (sum, item) {
          return sum + item;
        });

        return result;
      } else {
        return 0;
      }
    }
  },
}
</script>

<style lang="scss">
  .v-cart {
    &__back {
      position: absolute;
      top: 10px;
      right: 10px;
      padding: $padding * 2;
      border: 1px solid #aeaeae;
    }

    &__list {
      margin-bottom: 110px;
    }

    &__total {
      position: fixed;
      bottom: 0;
      left: 0;
      right: 0;
      padding: $padding * 2 $padding * 3;
      display: flex;
      justify-content: center;
      background-color: #26ae68;
      color: #ffffff;
      font-size: 20px;
    }
  }

  .total__name {
    margin-right: $margin * 2;
  }
</style>
