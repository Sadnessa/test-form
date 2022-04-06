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
    <div class="errors">
      <div class="error" v-for="error in v.$errors" :key="error.$uid">
        {{ error.$message }}
      </div>
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
        "input--ex": !this.v.$error,
      };
    },
  },
};
</script>

<style lang="scss" scoped>
.input {
  display: flex;
  padding: 4px;
  background: rgb(236, 236, 236);
  border-radius: 4px;
  width: 100%;
  box-sizing: border-box;
  margin-bottom: 2px;

  &--error {
    background: rgba(255, 0, 0, 0.137);
    outline: 1px solid rgba(253, 46, 46, 0.527);
  }

  &--ex {
    &:focus-within {
      background: rgba(0, 255, 21, 0.137);
      outline: 1px solid rgba(76, 201, 103, 0.788);
    }
  }

  input {
    width: 100%;
    border: none;
    background: transparent;
    padding: 4px;
    font-family: "Roboto", sans-serif;

    &:focus {
      outline: none;
    }
  }
}

.errors {
  display: flex; 
  justify-content: center;
  width: 100%;
  height: 10px;
  font-size: 10px;
  padding-top: 2px;
  color: rgba(255, 20, 20, 0.699);
  font-weight: bold;

  .error {
    padding-right: 10px;

    &:last-child {
      padding-right: 0px;
    }
  }
}
</style>