<template>
  <div class="input">
    <input />
    <slot name="icon"></slot>
  </div>
</template>

<style lang="scss" scoped>
.input {
  display: flex;
  padding: 4px;
  background: rgb(212, 212, 212);
  border-radius: 4px;
  width: 100%;
  box-sizing: border-box;

  input {
    width: 100%;
    border: none;
    background: transparent;
    padding: 4px;

    &:focus {
      outline: none;
    }
  }
}
</style>