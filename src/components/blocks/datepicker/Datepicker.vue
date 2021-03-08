<template>
  <div class="datepicker__mainContainer">
    <label class="datepicker__label" :for="'datepicker-id-' + this.datepickName">{{ this.datepickLabel }}</label>
    <input class="datepicker__input" :min="this.min" type="date" :id="'datepicker-id-' + this.datepickName" v-model="this.value" @change="this.emitChange" >
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
    },
    min: {
      type: Date
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
@import './datepicker.scss'
</style>
