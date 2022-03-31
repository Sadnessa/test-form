<template>
  <div class="address">
     <p>Индекс</p>
    <FormInput></FormInput>
    <p>Страна</p>
    <FormInput></FormInput>
    <p>Область</p>
    <FormInput></FormInput>
    <p>Город</p>
    <FormInput></FormInput>
    <p>Улица</p>
    <FormInput></FormInput>
    <p>Дом</p>
    <FormInput></FormInput>
  </div>
</template>

<script>
import FormInput from "./base/FormInput.vue";
export default {
  components: {
    FormInput
  }
}
</script>