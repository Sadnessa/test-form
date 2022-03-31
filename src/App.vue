<template>
  <FormCard>
    <div class="scroll">
      <About></About>
      <Address></Address>
      <Passport></Passport>
      <!-- <About></About> -->
    </div>
  </FormCard>
</template>

<script>
import FormCard from "./components/base/FormCard.vue";
import About from "./components/About.vue";
import Address from "./components/Address.vue";
import Passport from "./components/Passport.vue";

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
  margin: 0px;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0px 60px;
  overflow: hidden;
}
</style>

<style lang="scss" scoped>
.card {
  width: 100%;
  max-width: 400px;
  height: 100%;
  max-height: 600px;
  overflow: hidden;

  .scroll {
    height: 100%;
    overflow-y: auto;
    // scrollbar-gutter: stable;
  }
}
</style>
