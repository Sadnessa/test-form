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
    <FormSelector icon="expand_more" :doctors="doc"></FormSelector>
   <p> Не отправлять СМС.</p>
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
    return  {
      doc: ["Иванов", "Захаров", "Чернышова"]
    }
  }
};
</script>