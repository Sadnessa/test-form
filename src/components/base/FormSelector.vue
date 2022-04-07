<template>
  <div class="selector">
    <FormInput
      readOnly
      @click="clickSelect"
      :modelValue="computedInputText"
      :v="v"
    >
      <template #icon>
        <div class="icon">
          <span class="material-icons-round" v-if="isVisible">
            expand_less
          </span>
          <span class="material-icons-round" v-else> expand_more </span>
        </div>
      </template>
    </FormInput>
    <div class="select" v-if="isVisible" @click="onSelectorClick">
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
      clicked: false,
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

    v: {
      type: Object,
      default: {},
    },
  },

  mounted() {
    window.addEventListener("click", this.onWindowClick);
  },
  beforeUnmount() {
    window.removeEventListener("click", this.onWindowClick);
  },

  methods: {
    clickSelect() {
      this.isVisible = !this.isVisible;
      this.clicked = true
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

    onWindowClick() {
      if(this.clicked === false ) {
        this.isVisible = false;
      }
      
      this.clicked = false
    },

    onSelectorClick() {
      if(this.multiple) {
        this.clicked = true
      }
    }
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

    isVisible(newValue) {
      if (!newValue) {
        this.v.$validate;
      }
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
    top: 34px;
    width: 100%;
    padding: 4px 10px;
    border-bottom-right-radius: 10px;
    border-bottom-left-radius: 10px;
    max-width: 360px;
    background: white;
    box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;

    &__item {
      position: relative;
      display: flex;
      padding-top: 6px;
      padding-bottom: 4px;
      transition: 0.2s all ease-in-out;
      cursor: pointer;
      user-select: none;
      margin-bottom: 2px;

      p {
        font-weight: 300;
      }

      &:after {
        position: absolute;
        content: "";
        bottom: 0px;
        width: 100%;
        height: 1px;
        background: rgb(206, 206, 206);
      }

      // &:first-child {
      //   &:after {
      //     height: 2px;
      //   }
      // }

      &:last-child {
        margin-bottom: 0px;
        &:after {
          height: 0px;
        }
      }

      &:hover {
        background: rgba(192, 192, 192, 0.219);
        border-radius: 6px;
      }

      p {
        margin: 0px;
        padding: 2px 6px;
      }
    }
  }
}
</style>