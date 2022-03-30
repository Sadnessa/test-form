<template>
  <FormCard></FormCard>
</template>

<script>
import FormCard from "./components/FormCard.vue";
export default {
  components: {
    FormCard,
  },
};
</script>

<style>
body {
  background: rgb(212, 212, 212);
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0px 60px;
}
</style>
