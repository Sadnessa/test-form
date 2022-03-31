<template>
  <div class="selector">
    <FormInput>
      <template #icon>
        <span class="material-icons-round" @click="clickSelect">
          {{ icon }}
        </span>
      </template>
    </FormInput>
    <div class="select" v-if="isVisible">
      <div class="select__item" v-for="i in doctors" :key="i">
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

  data() {
    return {
      isVisible: false,
    };
  },

  props: {
    icon: {
      type: String,
    },

    doctors: {
      type: Array,
    },
  },

  methods: {
    clickSelect() {
      if (this.isVisible === false) {
        this.isVisible = true;
      } else {
        this.isVisible = false;
      }
    },
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

    &__item {
      border-bottom: solid 2px rgb(206, 206, 206);
    }
  }
}
</style>