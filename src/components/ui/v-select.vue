<template>
  <div class="v-select">
    <span
        class="v-select__title"
        @click="areOptionsVisible = !areOptionsVisible"
    >{{ currentSelectValue }}</span>
    <div
        class="v-select__options"
        v-if="areOptionsVisible"
    >
      <span
        class="v-select__option"
        v-for="option in options"
        :key="option.value"
        @click="selectOption(option)"
      >
        {{ option.name }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "v-select",
  data: () => ({
    areOptionsVisible: false
  }),
  props: {
    options: {
      type: Array,
      default() {
        return [];
      }
    },
    currentSelectValue: {
      type: String,
      default() {
        return '';
      }
    }
  },
  methods: {
    selectOption(option) {
      this.$emit('changeSelect', option);
      this.hideSelect();
    },
    hideSelect() {
      this.areOptionsVisible = false;
    }
  },
  mounted() {
    document.addEventListener('click', this.hideSelect.bind(this), true);
  },
  beforeUnmount() {
    document.removeEventListener('click', this.hideSelect.bind(this));
  }
}
</script>

<style lang="scss">
  .v-select {
    position: relative;
    width: 200px;

    &__title {
      display: block;
      border: 1px solid #aeaeae;
      user-select: none;
      cursor: pointer;
    }

    &__options {
      position: absolute;
      top: 20px;
      left: 0;
      width: 100%;
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      border: 1px solid #aeaeae;
      background-color: #ffffff;
      box-sizing: border-box;
    }

    &__option {
      width: 100%;
      cursor: pointer;

      &:hover {
        background-color: #e7e7e7;
      }
    }
  }
</style>
