<template>
  <div class="v-main-wrapper">
    <v-catalog/>
    <v-cart/>
  </div>
</template>

<script>
import vCatalog from '@/components/v-catalog';
import vCart from '@/components/v-cart';

export default {
  name: "v-main-wrapper",
  components: {
    vCatalog,
    vCart,
  },
  props: {},
  data: () => ({
    title: 'Main wrapper',
  }),
  computed: {},
  methods: {},
  watch: {},
  mounted() {
    console.log('!');
  }
}
</script>

<style>
  .v-main-wrapper {
    display: flex;
    justify-content: center;
    align-content: center;
    flex-direction: column;
    max-width: 900px;
    margin: 0 auto;
  }
</style>
