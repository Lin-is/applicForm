<template>
  <button
    class="button__btnElem"
    :class="this.className"
    @click="this.$emit('on-click')"
  >
  <p class="button__innerText">{{ this.btnTitle }}</p>
  </button>
</template>

<script>
export default {
  props: {
    btnTitle: {
      type: String,
      required: true
    },
    btnIsNext: {
      type: String,
      required: true
    }
  },
  computed: {
    className () {
      return (this.btnIsNext + '' === 'true'
        ? 'button__btnElem_next'
        : 'button__btnElem_prev')
    }
  }
}
</script>

<style lang="scss">
  @import './button.scss'
</style>
