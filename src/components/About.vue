<template>
  <div class="about">
    <p>Фамилия*</p>
    <FormInput></FormInput>
    <p>Имя*</p>
    <FormInput></FormInput>
    <p>Отчество</p>
    <FormInput></FormInput>
    <p>Дата рождения*</p>
    <FormInput></FormInput>
    <p>Номер телефона*</p>
    <FormInput></FormInput>
    <p>Пол</p>
    <p>Группа клиентов*.</p>
    <p>Лечащий врач.</p>
    <FormSelector :doctors="doc"></FormSelector>
    <label><input type="checkbox" />Не отправлять СМС.</label>
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

  data() {
    return {
      doc: ["Иванов", "Захаров", "Чернышова"],
    };
  },
};
</script>

<style lang="scss" scoped>
.about {
  box-sizing: border-box;
}
</style>