<template>
  <div class="input">
    <input v-model="modelValue" @update:modelValue="onInput" />
    <slot name="icon"></slot>
  </div>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: String,
    }
  },

  methods: {
    onInput(event) {
      this.$emit("update:modelValue", event)
    }
  }
}
</script>

<style lang="scss" scoped>
.input {
  display: flex;
  padding: 4px;
  background: rgb(224, 224, 224);
  border-radius: 4px;
  width: 100%;
  box-sizing: border-box;
  margin-bottom: 12px;

  input {
    width: 100%;
    border: none;
    background: transparent;
    padding: 4px;

    &:focus {
      outline: none;
    }
  }
}
</style>