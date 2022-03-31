<template>
  <div class="selector">
    <FormInput>
      <template #icon>
        <span class="material-icons-round"> {{ icon }} </span>
      </template>
    </FormInput>
    <div class="select">
      <div class="select__item" v-for="i in doctors" :key=i>
        {{ i }}
        </div>
    </div>
  </div>
</template>

<script>
import FormInput from "./FormInput.vue";
export default {
  components: {
    FormInput,
  },

  props: {
    icon: {
      type: String,
    },

    doctors: {
      type: Array,
    }
  },
};
</script>

<style lang="scss" scoped>
.selector {
  position: relative;

  span {
    user-select: none;
    cursor: pointer;
  }

  .select {
    position: absolute;
    width: 100%;
    background: white;
  }
}
</style>