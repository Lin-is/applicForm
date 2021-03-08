<template>
  <div class="input__mainContainer">
    <label class="input__label" for="">{{ this.label }}</label>
    <input
      class="input__inputElem"
      @change="this.$emit('get-value', {name: this.name, value: this.value})"
      :name="this.name"
      v-model="value"
      type="text"
      :placeholder="this.placeholder"
    />
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      required: true
    },
    placeholder: {
      type: String,
      required: true
    },
    name: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      value: null
    }
  }
}
</script>

<style lang="scss">
  @import './input.scss'
</style>
