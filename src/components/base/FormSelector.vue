<template>
  <FormInput>
    <template #icon>
      <span class="material-icons-round"> {{ icon }} </span>
    </template>
  </FormInput>
</template>

<script>
import FormInput from "./FormInput.vue";
export default {
  components: {
    FormInput,
  },

  props: {
    icon: {
      type: String,
    },
  },
};
</script>

<style lang="scss" scoped>
span {
  user-select: none;
  cursor: pointer;
}
</style>