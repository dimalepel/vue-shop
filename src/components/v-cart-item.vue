<template>
  <div class="v-cart-item">
    <img class="v-cart-item__image" :src="require('../assets/images/' + cart_item_data.image)" alt="img">
    <div class="v-cart-item__info">
      <p>{{ cart_item.name }}</p>
      <p>Price: {{ cart_item.price }} $</p>
      <p>{{ cart_item.article }}</p>
    </div>
    <div class="v-cart-item__quantity">
      <p>Qty:&nbsp;</p>
      {{ cart_item.quantity }}
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
    deleteFromCart() {
      this.$emit('deleteFromCart');
    },
  },
  mounted() {
    this.cart_item.quantity = 1;
  }
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

    &__quantity {
      display: flex;
      align-items: center;
    }
  }
</style>
