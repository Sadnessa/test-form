<template>
  <FormCard>
    <div class="view">
      <div class="view__item" v-for="i in forms" :key="i">
        {{ i }}
      </div>
    </div>
    <div class="content">
      <About v-if="currentForm == 0"></About>
      <Address v-if="currentForm == 1"></Address>
      <Passport v-if="currentForm == 2"></Passport>
      <button @click="prevButton" v-if="this.currentForm >= 1">Prev</button>
      <button @click="nextButton" v-if="this.currentForm <= 1">Next</button>
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

  data() {
    return {
      forms: [1, 2, 3],
      currentForm: 0,
    };
  },

  methods: {
    prevButton() {
      if (this.currentForm <= 0) {
        return;
      }
      this.currentForm--;
    },

    nextButton() {
      if (this.currentForm >= 2) {
        return;
      }
      this.currentForm++;
    },
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

p {
  margin: 0px;
  margin-bottom: 8px;
}
</style>

<style lang="scss" scoped>
.card {
  display: flex;
  flex-direction: column;
  width: 100%;
  max-width: 400px;
  height: 100%;
  max-height: 600px;
  overflow: hidden;

  .view {
    display: flex;
    justify-content: space-around;
    padding: 6px 0px;
  }

  .content {
    flex-grow: 1;
    padding: 8px;
    box-sizing: border-box;
  }
}
</style>
