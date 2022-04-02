<template>
  <div class="passport">
    <p>Тип документа</p>
    <FormSelector :items="documents" v-model="modelValue.documents"></FormSelector>
    <p>Серия</p>
    <FormInput v-model="modelValue.series"></FormInput>
    <p>Номер</p>
    <FormInput v-model="modelValue.no"></FormInput>
    <p>Кем выдан</p>
    <FormInput v-model="modelValue.authory"></FormInput>
    <p>Дата выдачи</p>
    <FormInput v-model="modelValue.date"></FormInput>
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
    }
  },

  data() {
    return {
      documents: ["Паспорт", "Свидетельство о рождении", "Водительские права"],
    };
  },
};
</script>