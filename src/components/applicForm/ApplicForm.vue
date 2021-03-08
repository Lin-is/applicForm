<template>
  <form class="applicForm__container" action="submit" @submit.prevent>
    <!-- step 1 section -->
    <section class="applicForm__stepContainer applicForm__stepContainer_step1">
      <h2 class="appplicForm__stepHeader">Шаг 1.</h2>

      <section class="applicForm__optionsContainer">
        <div class="applicForm__optionsLine">

          <div class="applicForm__optionContainer applicForm__optionContainer_countries">
            <Selector selectName="countries" :options="this.selectData.countries" label="Выберите страну" @getValue="gotSelectValue"  />
          </div>

          <div class="applicForm__optionContainer applicForm__optionContainer_types">
            <Selector selectName="types" :options="this.selectData.types" label="Тип визы" @getValue="gotSelectValue"  />
          </div>

        </div>
        <!-- end of first optionsLine -->
        <div class="applicForm__optionsLine">

          <div class="applicForm__optionContainer applicForm__optionContainer_entryDate">
            <Datepicker datepickName="entryDate" datepickLabel="Въезд" />
            <Datepicker datepickName="departureDate" datepickLabel="Выезд" />
          </div>

          <div class="applicForm__optionContainer applicForm__optionContainer_try">
            <Selector selectName="try" :options="this.selectData.try" label="Количество заездов" @getValue="gotSelectValue"  />
          </div>

          <div class="applicForm__optionContainer applicForm__optionContainer_timespent">
            <Selector selectName="timespent" :options="this.selectData.timespent" label="Время обработки" @getValue="gotSelectValue"  />
          </div>

        </div>
        <!-- end of sec optionsLine -->
      </section>
      <!-- end of optionsContainer section -->
      <section class="applicForm__resultsContainer">
        <div class="applicForm__outputArea">
          <div class="appplicForm__costContainer">
            <p class="applicForm__prelimText">
              Предварительная<br/>
              стоимость:
            </p>
            <p class="applicForm__prelimTotal">€10.99</p>
          </div>
        </div>
        <Button btnTitle="Продолжить" btnIsNext="true"/>
      </section>
      <!-- end of resultsContainer section -->
    </section>
    <!-- end of step 1 section -->
    <!-- step 2 section -->
    <section class="applicForm__stepContainer">
    </section>
    <!-- end of step 1 section -->
  </form>
</template>

<script>
import data from '../../assets/data.json'
import Selector from '../blocks/select/Selector.vue'
// import Input from './components/blocks/input/Input.vue'
import Button from '../blocks/button/Button.vue'
import Datepicker from '../blocks/datepicker/Datepicker.vue'

export default {
  components: {
    Selector, Button, Datepicker
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
  },
  compued: {
    filteredTypes () {
      return [{}]
    },
    filteredTimespent () {
      return [{}]
    },
    preliminaryCost () {
      return ''
    }
  }
}

</script>

<style lang="scss">
@import './applicForm.scss';
</style>
