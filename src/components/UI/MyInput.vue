<template>
  <input
      :value="modelValue" @input="updateInput" class="input" type="text">
</template>

<script>
export default {
  name: "my-input",
  props: {
    modelValue: [String, Number]
  },
  methods: {
    updateInput(event) {
      this.$emit("update:modelValue", event.target.value)
    }
  }
}
</script>

<style scoped lang="scss">
.input {
  width: 100%;
  border: 1px solid darkslateblue;
  padding: 10px;
  margin-top: 10px;
  outline: none;

  &:focus {
    border: 2px solid darkslateblue;
  }
}
</style>