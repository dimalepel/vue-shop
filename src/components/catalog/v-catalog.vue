<template>
  <div class="v-catalog">
    <router-link :to="{ name: 'cart' }">
      <div class="v-catalog__cart-lik">Cart: {{ CART.length }}</div>
    </router-link>

    <h1>Catalog</h1>

    <div class="v-catalog__list">
      <v-catalog-item
        v-for="product in PRODUCTS"
        :key="product.article"
        :product_data="product"
        @addToCart="addToCart"
      />
    </div>

  </div>
</template>

<script>
import vCatalogItem from '@/components/catalog/v-catalog-item';
import { mapActions, mapGetters } from 'vuex';

export default {
  name: "v-catalog",
  components: {
    vCatalogItem,
  },
  methods: {
    ...mapActions([
      'GET_PRODUCTS_FROM_API',
      'ADD_TO_CART'
    ]),
    addToCart(data) {
      this.ADD_TO_CART(data);
    }
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API();
  },
  computed: {
    ...mapGetters([
      'PRODUCTS',
      'CART'
    ])
  }
}
</script>

<style lang="scss">
  .v-catalog {
    &__list {
       display: flex;
       flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
     }

    &__cart-lik {
      position: absolute;
      top: 10px;
      right: 10px;
      padding: $padding * 2;
      border: 1px solid #aeaeae;
    }
  }
</style>
