<template>
  <div class="datepicker__mainContainer">
    <label class="datepicker__label" :for="'datepicker-id-' + this.datepickName">{{ this.datepickLabel }}</label>
    <input class="datepicker__input" type="date" :id="'datepicker-id-' + this.datepickName" >
  </div>
</template>

<script>
export default {
  props: {
    datepickLabel: {
      type: String,
      required: true
    },
    datepickName: {
      type: String,
      required: true
    }
  }
}
</script>

<style lang="scss">
@import './datepicker.scss'
</style>
