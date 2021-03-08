<template>
  <div class="input__mainContainer">
    <label class="input__label" for="">{{ this.label }}</label>
    <input
      class="input__inputElem"
      @change="this.emitChange"
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
  },
  methods: {
    emitChange () {
      this.$emit('get-value', this.value)
    }
  }
}
</script>

<style lang="scss">
  @import './input.scss'
</style>
