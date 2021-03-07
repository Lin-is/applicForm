<template>
  <Selector selectName="countries" :options="this.selectData.countries" label="Выберите страну" @getValue="gotValue"  />
</template>

<script>
import data from './assets/data.json'
import Selector from './components/blocks/select/Selector.vue'

export default {
  components: {
    Selector
  },
  data () {
    return {
      selectData: data
    }
  },
  methods: {
    gotValue () {

    }
  }
}

</script>

<style lang="scss">
  #app {
    background: #3748AA;
    width: 100%;
    height: 100vh;
    padding: 0;
    margin: 0;
  }
</style>
