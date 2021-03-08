<template>
  <form class="applicForm__container" action="submit" @submit.prevent>
    <!-- step 1 section -->
    <section class="applicForm__stepContainer applicForm__stepContainer_step1">
      <h2 class="appplicForm__stepHeader">Шаг 1.</h2>
      <!-- optionsContainer section -->
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
      <!-- end of optionsContainer -->
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
      <!-- end of resultsContainer -->
    </section>
    <!-- end of step 1 section -->
    <!-- step 2 section -->
    <section class="applicForm__stepContainer applicForm__stepContainer_step2">
      <h2 class="appplicForm__stepHeader">Шаг 2.</h2>

      <p class="applicForm__userName">{{this.userName}}</p>

      <!-- optionsContainer -->
      <section class="applicForm__optionsContainer">
        <div class="applicForm__optionsLine">

          <div class="applicForm__optionContainer applicForm__optionContainer_name">
            <Input label="Имя" placeholder="Введите имя" name="name" @getValue="gotSelectValue"  />
          </div>

          <div class="applicForm__optionContainer applicForm__optionContainer_surname">
            <Input label="Фамилия" placeholder="Введите фамилию" name="surname" @getValue="gotSelectValue"  />
          </div>

          <div class="applicForm__optionContainer applicForm__optionContainer_birthDate">
            <Datepicker datepickName="birthDate" datepickLabel="Дата рождения" />
          </div>

          <div class="applicForm__optionContainer applicForm__optionContainer_citizenship">
            <Selector selectName="citizenship" :options="this.citizenshipList" label="Гражданство" @getValue="gotSelectValue"  />
          </div>

        </div>
      </section>
      <!-- end of optionsContainer -->
      <section class="applicForm__resultsContainer">
        <div class="applicForm__outputArea">
          <div class="applicForm__prevInfoContainer">
            <h4 class="applicForm__infoTitle">Виза</h4>
            <div class="applicForm__infoCell">
              <p class="applicForm__prevInfo">Страна: {{this.collectedInfo.entryCountry}}</p>
              <p class="applicForm__prevInfo">Вид визы: {{this.collectedInfo.visaType}}</p>
            </div>
            <div class="applicForm__infoCell">
              <p class="applicForm__prevInfo">Въезд: {{this.collectedInfo.entryDate}}</p>
              <p class="applicForm__prevInfo">Время обработки: {{this.collectedInfo.timespent}}</p>
            </div>
          </div>
          <div class="appplicForm__costContainer">
            <p class="applicForm__prelimText">
              Предварительная<br/>
              стоимость:
            </p>
            <p class="applicForm__prelimTotal">€10.99</p>
          </div>
        </div>
        <div class="applicForm__buttonsContainer">
          <div class="applicForm__btnContainer">
            <Button btnTitle="Вернуться" btnIsNext="false"/>
          </div>
          <Button btnTitle="Готово" btnIsNext="true"/>
        </div>
      </section>
      <!-- end of resultsContainer -->
    </section>
    <!-- end of step 2 section -->
  </form>
</template>

<script>
import data from '../../assets/data.json'
import Selector from '../blocks/select/Selector.vue'
import Input from '../blocks/input/Input.vue'
import Button from '../blocks/button/Button.vue'
import Datepicker from '../blocks/datepicker/Datepicker.vue'

export default {
  components: {
    Selector, Button, Datepicker, Input
  },
  data () {
    return {
      selectData: data,
      citizenshipList: [
        { id: 'RU', name: 'Россия' },
        { id: 'DE', name: 'Германия' },
        { id: 'EE', name: 'Эстония' }
      ],
      collectedInfo: {
        name: null,
        surname: null,
        birthDate: null,
        citizenship: null,
        entryCountry: null,
        visaType: null,
        entryDate: null,
        departureDate: null,
        entrancesNumber: null,
        timespent: null,
        cost: null
      }
    }
  },
  methods: {
    gotSelectValue () {

    },
    gotInputValue () {

    }
  },
  computed: {
    filteredTypes () {
      return [{}]
    },
    filteredTimespent () {
      return [{}]
    },
    preliminaryCost () {
      return ''
    },
    userName () {
      const name = 'Пользователь'
      return name
    }
  }
}

</script>

<style lang="scss">
@import './applicForm.scss';
</style>
