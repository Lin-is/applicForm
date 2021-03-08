<template>
  <Selector selectName="countries" :options="this.selectData.countries" label="Выберите страну" @getValue="gotSelectValue"  />
  <Input label="Имя" placeholder="Введите имя" name="name" @getValue="gotInputValue" />
  <Button btnTitle="Продолжить" btnIsNext="true"/>
  <Button btnTitle="Вернуться" btnIsNext="false"/>
  <Datepicker datepickName="birthDate" datepickLabel="Дата рождения"/>
</template>

<script>
import data from './assets/data.json'
import Selector from './components/blocks/select/Selector.vue'
import Input from './components/blocks/input/Input.vue'
import Button from './components/blocks/button/Button.vue'
import Datepicker from './components/blocks/datepicker/Datepicker.vue'

export default {
  components: {
    Selector, Input, Button, Datepicker
  },
  data () {
    return {
      selectData: data
    }
  },
  methods: {
    gotSelectValue () {

    },
    gotInputValue () {

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
