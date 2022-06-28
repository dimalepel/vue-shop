<template>
  <div class="v-cart-item">
    <img class="v-cart-item__image" :src="require('../assets/images/' + cart_item_data.image)" alt="img">
    <div class="v-cart-item__info">
      <p>{{ cart_item.name }}</p>
      <p>Price: {{ cart_item.price }} $</p>
      <p>{{ cart_item.article }}</p>
    </div>
    <div class="v-cart-item__quantity">
      <p>Qty:</p>
      <div class="v-cart-item__counter">
        <button @click="decrementItem" type="button">-</button>
        <span class="v-cart-item__digit">
          {{ cart_item.quantity }}
        </span>
        <button @click="incrementItem" type="button">+</button>
      </div>

    </div>
    <button class="v-cart-item__remove btn"
            @click="deleteFromCart"
    >Delete</button>
  </div>
</template>

<script>
export default {
  name: "v-cart-item",
  data() {
    return {
      cart_item: this.cart_item_data
    }
  },
  props: {
    cart_item_data: {
      type: Object,
      default() {
        return {};
      }
    }
  },
  methods: {
    decrementItem() {
      this.$emit('decrement');
    },
    incrementItem() {
      this.$emit('increment');
    },
    deleteFromCart() {
      this.$emit('deleteFromCart');
    },
  },
}
</script>

<style lang="scss">
  .v-cart-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: nowrap;
    box-shadow: 0 0 8px 0 #e0e0e0;
    padding: $padding * 2;
    margin-bottom: $margin * 2;

    &__image {
      max-width: 50px;
    }

    &__counter {
      display: flex;
      justify-content: center;
      align-items: center;

      & button {
        cursor: pointer;
      }
    }

    &__digit {
      width: 30px;
      text-align: center;
    }
  }
</style>
