<template>
  <FormCard>
    fdfd
    <About></About>
    <Address></Address>
    <Passport></Passport>
  </FormCard>
</template>

<script>
import FormCard from "./components/base/FormCard.vue"
import About from "./components/About.vue"
import Address from "./components/Address.vue"
import Passport from "./components/Passport.vue"

export default {
  components: {
    FormCard,
    About,
    Address,
    Passport,
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
