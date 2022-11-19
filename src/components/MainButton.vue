<template>
  <button class="base-button" :class="buttonType">{{ buttonTitle }}</button>
</template>

<script>
export default {
  name: "MainButton",
  props: {
    buttonType: String,
    buttonTitle: String,
  },
};
</script>

<style scoped>
.base-button {
  all: unset;
  border-radius: 5px;
  background-color: var(--color-accent-blue);
  box-shadow: 3px 3px var(--color-accent-pink);
  padding: 0.5em;
  color: var(--color-bg-input);
  border: 2px solid var(--color-accent-blue);
}
.base-button:hover {
  border: 2px solid var(--color-accent-yellow);
}
</style>
