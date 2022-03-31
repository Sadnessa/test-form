<template>
  <FormCard>
    fdfd
    <FormInput></FormInput>
    <FormSelector></FormSelector>
    <FormButton>fdfd</FormButton>
  </FormCard>
</template>

<script>
import FormCard from "./components/base/FormCard.vue";
import FormInput from "./components/base/FormInput.vue";
import FormSelector from "./components/base/FormSelector.vue"
import FormButton from "./components/base/FormButton.vue";

export default {
  components: {
    FormCard,
    FormInput,
    FormButton,
    FormSelector,
  },
};
</script>

<style>
body {
  background: rgb(212, 212, 212);
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0px 60px;
}
</style>

<style lang="scss" scoped>

</style>
