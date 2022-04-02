<template>
  <div class="address">
     <p>Индекс</p>
    <FormInput v-model="modelValue.postMail"></FormInput>
    <p>Страна</p>
    <FormInput v-model="modelValue.country"></FormInput>
    <p>Область</p>
    <FormInput v-model="modelValue.region"></FormInput>
    <p>Город</p>
    <FormInput v-model="modelValue.city"></FormInput>
    <p>Улица</p>
    <FormInput v-model="modelValue.street"></FormInput>
    <p>Дом</p>
    <FormInput v-model="modelValue.building"></FormInput>
  </div>
</template>

<script>
import FormInput from "./base/FormInput.vue";
export default {
  components: {
    FormInput
  },

  props: {
    modelValue: {
      type: Object,
    }
  }
}
</script>