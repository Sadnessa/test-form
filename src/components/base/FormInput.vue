<template>
  <div class="input-wrapper">
    <div class="input">
      <input :value="modelValue" @input="onInput" :readonly="readOnly" @blur="v.$validate"/>
      <slot name="icon"></slot>
    </div>
    <div class="error" v-for="error in v.$errors" :key="error.$uid">
      {{ error.$message }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    readOnly: {
      type: Boolean,
      default: false,
    },

    modelValue: {
      type: String,
    },

    v: {
      type: Object,
      default: {}
    },
  },

  methods: {
    onInput(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
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