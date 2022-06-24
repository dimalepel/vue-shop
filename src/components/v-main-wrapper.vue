<template>
  <div class="v-main-wrapper">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: "v-main-wrapper",
}
</script>

<style>
  .v-main-wrapper {
    max-width: 900px;
    margin: 0 auto;
  }
</style>
