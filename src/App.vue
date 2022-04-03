<template>
  <FormCard>
    <div class="view">
      <div class="view__item" v-for="i in forms" :key="i">
        {{ i }}
      </div>
    </div>
    <div class="content">
      <About v-if="currentForm == 0" v-model="about" :validations="v$"></About>
      <Address v-if="currentForm == 1" v-model="address"></Address>
      <Passport v-if="currentForm == 2" v-model="passport"></Passport>
    </div>
    <div class="btns">
      <div class="btns__wrapper">
        <FormButton @click="prevButton" v-if="this.currentForm >= 1">
          Назад
        </FormButton>
      </div>
      <div class="btns__wrapper">
        <FormButton @click="nextButton" v-if="this.currentForm <= 1">
          Далее
        </FormButton>
      </div>
    </div>
  </FormCard>
</template>

<script>
import useVuelidate from '@vuelidate/core'
import { required } from '@vuelidate/validators'

import FormCard from "./components/base/FormCard.vue";
import About from "./components/About.vue";
import Address from "./components/Address.vue";
import Passport from "./components/Passport.vue";
import FormButton from "./components/base/FormButton.vue";

export default {
  components: {
    FormCard,
    About,
    Address,
    Passport,
    FormButton,
  },

  setup () {
    return { v$: useVuelidate() }
  },

  data() {
    return {
      forms: [1, 2, 3],
      currentForm: 0,
      about: {
        lastName: "",
        firstName: "",
        patronymic: "",
        birth: "",
        phone: "",
        gender: "",
        client: "",
        doctor: "",
        sms: false,
      },
      address: {
        postMail: "",
        country: "",
        region: "",
        city: "",
        street: "",
        building: "",
      },
      passport: {
        document: "",
        series: "",
        no: "",
        authory: "",
        date: "",
      },
    };
  },

  validations() {
    return {
      about: {
        lastName: { required, $autoDirty: true },
        firstName: { required },
        patronymic: "",
        birth: { required },
        phone: { required },
        gender: "",
        client: { required },
        doctor: "",
        sms: false,
      },
      address: {
        postMail: "",
        country: "",
        region: "",
        city: { required },
        street: "",
        building: "",
      },
      passport: {
        document: { required },
        series: "",
        no: "",
        authory: "",
        date: { required },
      },
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

<style lang="scss">
body {
  background-color: #8ec5fc;
  background-image: linear-gradient(62deg, #8ec5fc 0%, #e0c3fc 100%);
  margin: 0px;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0px 20px;
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
  min-height: 650px;

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

  .btns {
    display: flex;

    &__wrapper {
      width: 100%;
      margin-right: 10px;

      &:last-child {
        margin-right: 0px;
      }
    }
  }
}
</style>
