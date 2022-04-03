<template>
    <div class="modal">
      <FormCard class="modal__window">
        <slot></slot>
        <FormButton @click="$emit('update:modelValue', false)">Ok</FormButton>
      </FormCard>
    </div>
</template>

<script>
import FormCard from "./FormCard.vue"
import FormButton from "./FormButton.vue"

export default {
  components: {
    FormCard,
    FormButton
  },

  modelValue: {
    type: Boolean,
  }
}
</script>

<style lang="scss" scoped>
.modal {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
  background: rgba(151, 151, 151, 0.3);

  &__window {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    width: 100%;
    max-width: 300px;
    height: 100%;
    max-height: 150px;

    button {
      width: 100%;
      max-width: 150px;
      margin-top: 30px;
    }
  }
}
</style>