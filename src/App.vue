<template>
  <FormCard>
    <div class="view">
      <div
        class="view__item"
        v-for="i in forms"
        :key="i"
        :class="{ 'view__item--active': i - 1 == currentForm }"
        @click="currentForm = i - 1"
      >
        <div class="indicator"></div>
        {{ i }}
      </div>
    </div>

    <div class="content">
      <About v-if="currentForm == 0" v-model="about" :validations="v$"></About>

      <Address
        v-if="currentForm == 1"
        v-model="address"
        :validations="v$"
      ></Address>

      <Passport
        v-if="currentForm == 2"
        v-model="passport"
        :validations="v$"
      ></Passport>
    </div>

    <div class="btns">
      <div class="btns__wrapper">
        <FormButton @click="prevButton" v-if="this.currentForm >= 1">
          Назад
        </FormButton>
      </div>

      <div class="btns__wrapper" v-if="this.currentForm <= 1">
        <FormButton
          @click="nextButton"
          :disabled="currentFormValidation.$invalid"
        >
          Далее
        </FormButton>
      </div>

      <div class="btns__wrapper" v-if="this.currentForm == 2">
        <FormButton @click="onSave" :disabled="currentFormValidation.$invalid">
          Сохранить
        </FormButton>
      </div>
    </div>
  </FormCard>
  <FormModal v-if="doShowModal" v-model="doShowModal">
    <p>Новый клиент успешно создан</p>
  </FormModal>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import { required, maxLength, minLength, numeric, helpers } from "@vuelidate/validators";

import FormCard from "./components/base/FormCard.vue";
import About from "./components/About.vue";
import Address from "./components/Address.vue";
import Passport from "./components/Passport.vue";
import FormButton from "./components/base/FormButton.vue";
import FormModal from "./components/base/FormModal.vue";

const myRequired = helpers.withMessage("Поле обязательно к заполнению", required)
const myNumeric = helpers.withMessage("Необходимо использовать цифры", numeric)

export default {
  components: {
    FormCard,
    About,
    Address,
    Passport,
    FormButton,
    FormModal,
  },

  setup() {
    return { v$: useVuelidate() };
  },

  data() {
    return {
      forms: [1, 2, 3],
      currentForm: 0,
      doShowModal: false,
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
        lastName: { myRequired },
        firstName: { myRequired },
        patronymic: "",
        birth: { myRequired, myNumeric},
        phone: {
          myRequired,
          maxLength: maxLength(10),
          minLength: minLength(10),
          myNumeric,
        },
        gender: "",
        client: { myRequired },
        doctor: "",
        sms: false,
      },
      address: {
        postMail: "",
        country: "",
        region: "",
        city: { myRequired },
        street: "",
        building: "",
      },
      passport: {
        document: { myRequired },
        series: "",
        no: "",
        authory: "",
        date: { myRequired, myNumeric },
      },
    };
  },

  computed: {
    currentFormValidation() {
      if (this.currentForm === 0) {
        return this.v$.about;
      }
      if (this.currentForm === 1) {
        return this.v$.address;
      }
      if (this.currentForm === 2) {
        return this.v$.passport;
      }
    },
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

    onSave() {
      this.doShowModal = true;
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap");

body {
  background-color: #8ec5fc;
  background-image: linear-gradient(62deg, #8ec5fc 0%, #e0c3fc 100%);
  margin: 0px;
  font-family: "Roboto", sans-serif;
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
  margin: 0px 6px 8px;
  font-weight: bold;
  font-size: 14px;

  &:first-child {
    margin-top: 4px;
  }
}

label {
  font-size: 14px;
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

    &__item {
      position: relative;
      display: flex;
      align-items: center;
      flex-direction: column;
      width: 100%;
      transition: all ease-in-out 0.5s;
      padding: 6px 0px;
      cursor: pointer;

      .indicator {
        position: absolute;
        top: 0px;
        height: 4px;
        width: 100%;
        background: #ececec;
        border-radius: 6px 0px;
      }

      &:hover {
        background: #4f69dd0e;
      }

      &--active {
        background: #4f69dd1c;

        .indicator {
          background: #5ca1e6;
          background-image: linear-gradient(62deg, #8ec5fc 0%, #e0c3fc 100%);
        }
      }
    }
  }
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
</style>
