<template>
  <div class="selector">
    <FormInput @click="clickSelect" :modelValue="computedInput">
      <template #icon>
        <div class="icon">
          <span class="material-icons-round" v-if="isVisible">
            expand_less
          </span>
          <span class="material-icons-round" v-else> expand_more </span>
        </div>
      </template>
    </FormInput>
    <div class="select" v-if="isVisible">
      <div class="select__item" v-for="i in items" :key="i" @click="selectedItem = i">
        <p>{{ i }}</p>
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
      selectedItem: null,
    };
  },

  props: {
    items: {
      type: Array,
    },
  },

  methods: {
    clickSelect() {
      this.isVisible = !this.isVisible;
    },
  },

  computed: {
    computedInput() {
      if(this.selectedItem == null) {
        return this.selectedItem = "Выберите вариант ответа"
      }
      return this.selectedItem
    }
  },
};
</script>

<style lang="scss" scoped>
.selector {
  position: relative;
  z-index: 1;

  span {
    display: flex;
    justify-content: center;
    align-items: center;
    user-select: none;
    cursor: pointer;
    font-size: 22px;
  }

  .select {
    position: absolute;
    top: 32px;
    width: 100%;
    background: white;
    box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;

    &__item {
      padding-top: 6px;
      transition: 0.2s all ease-in-out;
      cursor: pointer;
      border-bottom: solid 2px rgb(206, 206, 206);

      &:last-child {
        border-bottom: none;
      }

      &:hover {
        background: rgba(192, 192, 192, 0.219);
      }

      p {
        margin: 0px;
        padding: 2px 6px;
      }
    }
  }
}
</style>