<template>
  <div class="input-wrapper">
    <div class="input" :class="computedInputClass">
      <input
        :value="modelValue"
        @input="onInput"
        :readonly="readOnly"
        @blur="v.$validate"
      />
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
      default: {},
    },
  },

  methods: {
    onInput(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },

  computed: {
    computedInputClass() {
      return {
        "input--error": this.v.$invalid && this.v.$dirty,
        "input--ex": !this.v.$error
      };
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

  &--error {
    background: rgba(255, 0, 0, 0.192);
    outline: 1px solid red;
  }

  &--ex {
    &:focus-within {
    background: rgba(0, 255, 21, 0.192);
    outline: 1px solid rgb(0, 165, 36);
  }
  }

  
}
</style>