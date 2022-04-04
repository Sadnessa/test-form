<template>
  <button :class="buttonStyle" :disabled="disabled">
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: {
    disabled: {
      type: Boolean,
      default: false,
    },
  },

  computed: {
    buttonStyle() {
      return {
        disabled: this.disabled,
        flat: this.flat,
      };
    },
  },
};
</script>

<style lang="scss" scoped>
button {
  position: relative;
  width: 100%;
  padding: 8px 12px;
  border: none;
  border-radius: 4px;
  background: #a57bff;
  color: white;
  font-weight: 700;
  z-index: 0;

  &:after {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0px;
    left: 0px;
    content: "";
    background: rgba(255, 255, 255, 0.2);
    transition: 0.3s all ease-in-out;
    opacity: 0;
  }

  &:hover::after {
    opacity: 1;
  }

  &.disabled {
    cursor: not-allowed;
    transition: none;

    &:after {
      opacity: 1;
      background: rgba(255, 255, 255, 0.5);
    }
  }
}
</style>