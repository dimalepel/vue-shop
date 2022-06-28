<template>
  <div class="v-catalog">
    <router-link :to="{ name: 'cart' }">
      <div class="v-catalog__cart-lik">Cart: {{ CART.length }}</div>
    </router-link>

    <h1>Catalog</h1>

    <v-select
      :options="options"
      :currentSelectValue="currentSelectValue"
      @changeSelect="changeSelect"
    />

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
import vSelect from '@/components/ui/v-select';
import { mapActions, mapGetters } from 'vuex';

export default {
  name: "v-catalog",
  data: () => ({
    currentSelectValue: 'Select',
    options: [
      { name: 'Option 1', value: 1 },
      { name: 'Option 2', value: 2 },
      { name: 'Option 3', value: 3 },
      { name: 'Option 4', value: 4 },
      { name: 'Option 5', value: 5 },
    ]
  }),
  components: {
    vCatalogItem,
    vSelect
  },
  methods: {
    ...mapActions([
      'GET_PRODUCTS_FROM_API',
      'ADD_TO_CART'
    ]),
    addToCart(data) {
      this.ADD_TO_CART(data);
    },
    changeSelect(option) {
      this.currentSelectValue = option.name;
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
