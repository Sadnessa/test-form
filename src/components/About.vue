<template>
  <div class="about">
    <p>Фамилия*</p>
    <FormInput v-model="modelValue.lastName"></FormInput>
    <p>Имя*</p>
    <FormInput v-model="modelValue.firstName"></FormInput>
    <p>Отчество</p>
    <FormInput v-model="modelValue.patronymic"></FormInput>
    <p>Дата рождения*</p>
    <FormInput v-model="modelValue.birth"></FormInput>
    <p>Номер телефона*</p>
    <FormInput v-model="modelValue.phone"></FormInput>
    <p>Пол</p>
    <div class="about__gender">
      <label>Женский<input v-model="modelValue.gender" type="radio" name="rad" value="Женский" /></label>
      <label>Мужской <input v-model="modelValue.gender" type="radio" name="rad" value="Мужской" /></label>
    </div>
    <p>Группа клиентов*.</p>
    <FormSelector
      multiple
      :items="clients"
      v-model="modelValue.client"
    ></FormSelector>
    <p>Лечащий врач.</p>
    <FormSelector :items="doctors" v-model="modelValue.doctor"></FormSelector>
    <label><input type="checkbox" v-model="modelValue.sms" />Не отправлять СМС.</label>
  </div>
</template>

<script>
import FormInput from "./base/FormInput.vue";
import FormSelector from "./base/FormSelector.vue";

export default {
  components: {
    FormInput,
    FormSelector,
  },

  props: {
    modelValue: {
      type: Object,
    },
  },

  emits: [],

  data() {
    return {
      doctors: ["Иванов", "Захаров", "Чернышова"],
      clients: ["VIP", "Проблемные", "ОМС"],
    };
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
    margin-bottom: 12px;
  }
}
</style>