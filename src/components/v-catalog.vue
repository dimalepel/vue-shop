<template>
  <div class="v-catalog">
    <h1>Catalog</h1>

    <div class="v-catalog__list">
      <v-catalog-item
        v-for="product in PRODUCTS"
        :key="product.article"
        :product_data="product"
        @sendArticle="sendArticle"
      />
    </div>

  </div>
</template>

<script>
import vCatalogItem from '@/components/v-catalog-item';
import { mapActions, mapGetters } from 'vuex';

export default {
  name: "v-catalog",
  data: () => ({}),
  components: {
    vCatalogItem,
  },
  methods: {
    ...mapActions([
      'GET_PRODUCTS_FROM_API',
    ]),
    sendArticle(data) {
      console.log(data);
    }
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API()
    .then((response) => {
      console.log(response.data);
    });
  },
  computed: {
    ...mapGetters([
      'PRODUCTS'
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
  }
</style>
