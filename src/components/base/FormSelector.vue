<template>
  <div class="selector">
    <FormInput readOnly @click="clickSelect" :modelValue="computedInputText">
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
      <div
        class="select__item"
        v-for="item in items"
        :key="item"
        @click="onItemClick(item)"
      >
        <input
          type="checkbox"
          v-if="multiple"
          :checked="isSelectedItem(item)"
        />
        <p>{{ item }}</p>
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

    multiple: {
      type: Boolean,
      default: false,
    },
  },

  methods: {
    clickSelect() {
      this.isVisible = !this.isVisible;
    },

    onItemClick(item) {
      if (!this.multiple) {
        this.selectedItem = item;
        return;
      }

      if (this.selectedItem == null) {
        this.selectedItem = [];
      }

      if (this.isSelectedItem(item)) {
        this.selectedItem = this.selectedItem.filter((i) => i !== item);
        return;
      }

      this.selectedItem.push(item);
    },

    isSelectedItem(item) {
      if (Array.isArray(this.selectedItem)) {
        return this.selectedItem.includes(item);
      }
    },
  },

  computed: {
    computedInputText() {
      if (this.selectedItem == null || this.selectedItem.length == 0) {
        return "Выберите вариант ответа";
      }

      if (Array.isArray(this.selectedItem)) {
        return this.selectedItem.join(", ");
      }

      return this.selectedItem;
    },
  },

  watch: {
    selectedItem(newValue) {
      this.$emit("update:modelValue", newValue);
    },
  },
};
</script>

<style lang="scss" scoped>
.selector {
  position: relative;

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
    z-index: 1;
    top: 32px;
    width: 100%;
    background: white;
    box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;

    &__item {
      display: flex;
      padding-top: 6px;
      transition: 0.2s all ease-in-out;
      cursor: pointer;
      user-select: none;
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