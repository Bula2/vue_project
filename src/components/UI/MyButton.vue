<template>
  <button class="button">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "my-button"
}
</script>

<style scoped lang="scss">
.button {
  width: 100px;
  background: none;
  color: darkslateblue;
  padding: 4px;
  border: 2px solid darkslateblue;
  border-radius: 4px;

  &:hover {
    border: 2px solid #8484ff;
  }
}
</style>