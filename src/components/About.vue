<template>
  <div class="about">
    <p>Фамилия*</p>
    <FormInput
      v-model="modelValue.lastName"
      :v="validations.about.lastName"
    ></FormInput>

    <p>Имя*</p>
    <FormInput
      v-model="modelValue.firstName"
      :v="validations.about.firstName"
    ></FormInput>

    <p>Отчество</p>
    <FormInput v-model="modelValue.patronymic"></FormInput>

    <p>Дата рождения*</p>
    <FormInput v-model="dateMask" :v="validations.about.birth"></FormInput>

    <p>Номер телефона*</p>
    <FormInput v-model="modelValue.phone" :v="validations.about.phone"></FormInput>

    <p>Пол</p>
    <div class="about__gender">
      <label>
        Женский
        <input
          v-model="modelValue.gender"
          type="radio"
          name="rad"
          value="Женский"
        />
      </label>
      <label>
        Мужской
        <input
          v-model="modelValue.gender"
          type="radio"
          name="rad"
          value="Мужской"
        />
      </label>
    </div>

    <p>Группа клиентов*.</p>
    <FormSelector
      multiple
      :items="clients"
      v-model="modelValue.client"
      :v="validations.about.client"
    ></FormSelector>

    <p>Лечащий врач.</p>
    <FormSelector :items="doctors" v-model="modelValue.doctor"></FormSelector>

    <label>
      <input type="checkbox" v-model="modelValue.sms" />
      Не отправлять СМС.
    </label>
  </div>
</template>

<script>
import FormInput from "./base/FormInput.vue";
import FormSelector from "./base/FormSelector.vue";

//date mask
function formatDate(date) {
  return date
    .replaceAll("/", "")
    .split("")
    .map((item, i) => {
      if ((i - 1) % 2 == 0 && i < 4) {
        return item + "/";
      }
      return item;
    })
    .slice(0, 8)
    .join("");
}

export default {
  components: {
    FormInput,
    FormSelector,
  },

  props: {
    modelValue: {
      type: Object,
    },

    validations: {
      type: Object,
      default: {},
    },
  },

  emits: [],

  data() {
    return {
      doctors: ["Иванов", "Захаров", "Чернышова"],
      clients: ["VIP", "Проблемные", "ОМС"],
    };
  },

  computed: {
    dateMask: {
      get() {
        return formatDate(this.modelValue.birth);
      },
      set(newDate) {
        this.modelValue.birth = newDate;
      },
    },
  },
};
</script>

<style lang="scss" scoped>
.about {
  box-sizing: border-box;

  &__gender {
    display: flex;
    & > * {
      width: 50%;
    }
    margin-bottom: 10px;
  }
}
</style>