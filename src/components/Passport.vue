<template>
  <div class="passport">
    <p>Тип документа</p>
    <FormSelector :items="documents"></FormSelector>
    <p>Серия</p>
    <FormInput></FormInput>
    <p>Номер</p>
    <FormInput></FormInput>
    <p>Кем выдан</p>
    <FormInput></FormInput>
    <p>Дата выдачи</p>
    <FormInput></FormInput>
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
      documents: ["Паспорт", "Свидетельство о рождении", "Водительские права"],
    };
  },
};
</script>