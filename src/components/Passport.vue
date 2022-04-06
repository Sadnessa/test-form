<template>
  <div class="passport">
    <p>Тип документа*:</p>
    <FormSelector
      :items="documents"
      v-model="modelValue.document"
      :v="validations.passport.document"
    ></FormSelector>

    <p>Серия:</p>
    <FormInput v-model="modelValue.series"></FormInput>

    <p>Номер:</p>
    <FormInput v-model="modelValue.no"></FormInput>

    <p>Кем выдан:</p>
    <FormInput v-model="modelValue.authory"></FormInput>

    <p>Дата выдачи*:</p>
    <FormInput
      v-model="dateMask"
      :v="validations.passport.date"
    ></FormInput>
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

  data() {
    return {
      documents: ["Паспорт", "Свидетельство о рождении", "Водительские права"],
    };
  },

  computed: {
    dateMask: {
      get() {
        return formatDate(this.modelValue.date);
      },
      set(newDate) {
        this.modelValue.date = newDate;
      },
    },
  },
};
</script>