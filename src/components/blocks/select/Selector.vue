<template>
  <div class="selector__mainContainer" :class="{'selector__mainContainer_open': this.inputIsActive}">
    <label class="selector__label">{{ this.label }}</label>
    <div class="selector__selectContainer">
      <input
        class="selector__input"
        :id="'selector__input-' + this.selectName"
        :class="{'selector__input_active': this.inputIsActive}"
        type="text"
        ref="selectInput"
        :value="this.value.name"
        :placeholder="this.label"
        @click="this.initSelection"
        @focus="this.$refs.select.focus()"
        readonly
      >
      <div
        class="selector__labelsContainer"
        :class="{'hidden': !this.inputIsActive}"
        ref="optionLabels"
      >
          <label
            class="selector__optionLabel"
            :class="{'selector__optionLabel_active': this.value === option.id}"
            v-for="(option, index) in this.options"
            :key="index"
            @click="this.selectOption"
            @keypress.enter="this.selectOption"
            :value="option.id"
            :id="'label-' + this.selectName + '-' + option.id"
          >
            {{ option.name }}
          </label>
      </div>
      <label class="selector__inputLabel" :for="'selector__input-' + this.selectName" />
      <select
        ref="select"
        class="selector__select"
        :class="{'selector__select_active': this.inputIsActive}"
        @keypress.enter="this.preventEnter"
        v-model="this.value"
        @change="this.emitChange"
      >
        <option
          class="selector__option"
          v-for="(option, index) in this.options"
          :label="option.name"
          :id="this.selectName+ '-' + option.id"
          :value="option.id"
          :key="index"
        />
      </select>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
      required: true
    },
    label: {
      type: String,
      require: true
    },
    selectName: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      value: {
        name: null
      },
      inputIsActive: false
    }
  },
  computed: {
  },
  methods: {
    emitChange () {
      this.$emit('get-value', this.value)
    },
    findOption (id) {
      const option = this.options.find(opt => opt.id === id)
      return option
    },
    selectOption (event) {
      const [,, optionId] = event.target.id.split('-')
      this.value = this.findOption(optionId)
      this.inputIsActive = false
      this.$refs.select.focus()
      this.emitChange()
    },
    initSelection () {
      this.$refs.select.focus()
      this.inputIsActive = !this.inputIsActive
    },
    preventEnter (event) {
      event.preventDefault()
      this.inputIsActive = !this.inputIsActive
    }
  }
}
</script>

<style lang="scss">
  @import './selector.scss';
</style>
