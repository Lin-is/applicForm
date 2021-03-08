<template>
  <div class="applicForm__triangle"></div>
  <div class="applicForm__formContainer">
    <form class="applicForm__formElem" :class="{'applicForm__formElem_moved': this.isSecondStep }" action="submit" @submit.prevent>
    <!-- step 1 -->
      <div class="applicForm__stepContainer applicForm__stepContainer_step1">
        <h2 class="appplicForm__stepHeader">Шаг 1.</h2>
        <!-- optionsContainer section -->
        <section class="applicForm__optionsContainer">
          <div class="applicForm__optionsLine">

            <div class="applicForm__optionContainer applicForm__optionContainer_countries">
              <Selector selectName="countries" :options="this.selectData.countries" label="Выберите страну" @getValue="getCountrie"  />
            </div>

            <div class="applicForm__optionContainer applicForm__optionContainer_types">
              <Selector selectName="types" :options="this.selectData.types" label="Тип визы" @getValue="getTypes"  />
            </div>

          </div>
          <!-- end of first optionsLine -->
          <div class="applicForm__optionsLine">

            <div class="applicForm__optionContainer applicForm__optionContainer_entryDate">
              <Datepicker datepickName="entryDate" datepickLabel="Въезд" @getValue="getEntryDate" />
              <Datepicker datepickName="departureDate" :min="this.minDate" datepickLabel="Выезд" @getValue="getDepartDate" />
            </div>

            <div class="applicForm__optionContainer applicForm__optionContainer_try">
              <Selector selectName="try" :options="this.filteredTry" label="Количество заездов" @getValue="getTry"  />
            </div>

            <div class="applicForm__optionContainer applicForm__optionContainer_timespent">
              <Selector selectName="timespent" :options="this.filteredTimespent" label="Время обработки" @getValue="getTimespent"  />
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
              <p class="applicForm__prelimTotal">{{ this.collectedInfo.cost }}</p>
            </div>
          </div>
          <Button btnTitle="Продолжить" btnIsNext="true" @onClick="toNextStep"/>
        </section>
        <!-- end of resultsContainer -->
      </div>
      <!-- end of step 1 -->
      <!-- step 2  -->
      <div class="applicForm__stepContainer applicForm__stepContainer_step2">
        <h2 class="appplicForm__stepHeader">Шаг 2.</h2>

        <p class="applicForm__userName">{{ this.userName }}</p>

        <!-- optionsContainer -->
        <section class="applicForm__optionsContainer">
          <div class="applicForm__optionsLine">

            <div class="applicForm__optionContainer applicForm__optionContainer_name">
              <Input label="Имя" placeholder="Введите имя" name="name" @getValue="getName"  />
            </div>

            <div class="applicForm__optionContainer applicForm__optionContainer_surname">
              <Input label="Фамилия" placeholder="Введите фамилию" name="surname" @getValue="getSurname"  />
            </div>

            <div class="applicForm__optionContainer applicForm__optionContainer_birthDate">
              <Datepicker datepickName="birthDate" datepickLabel="Дата рождения" @getValue="getBirthDate" />
            </div>

            <div class="applicForm__optionContainer applicForm__optionContainer_citizenship">
              <Selector selectName="citizenship" :options="this.citizenshipList" label="Гражданство" @getValue="getCitizenship"  />
            </div>

          </div>
        </section>
        <!-- end of optionsContainer -->
        <section class="applicForm__resultsContainer">
          <div class="applicForm__outputArea">
            <div class="applicForm__prevInfoContainer">
              <h4 class="applicForm__infoTitle">Виза</h4>
              <div class="applicForm__infoCell">
                <p class="applicForm__prevInfo">Страна: {{ this.collectedInfo.entryCountry ? this.collectedInfo.entryCountry.name : '' }}</p>
                <p class="applicForm__prevInfo">Вид визы: {{ this.collectedInfo.visaType ? this.collectedInfo.visaType.name : '' }}</p>
              </div>
              <div class="applicForm__infoCell">
                <p class="applicForm__prevInfo">Въезд: {{this.collectedInfo.entryDate ? this.collectedInfo.entryDate : '' }}</p>
                <p class="applicForm__prevInfo">Время обработки: {{ this.collectedInfo.timespent ? this.collectedInfo.timespent.name : '' }}</p>
              </div>
            </div>
            <div class="appplicForm__costContainer">
              <p class="applicForm__prelimText">
                Предварительная<br/>
                стоимость:
              </p>
              <p class="applicForm__prelimTotal">{{ this.collectedInfo.cost }}</p>
            </div>
          </div>
          <div class="applicForm__buttonsContainer">
            <div class="applicForm__btnContainer">
              <Button btnTitle="Вернуться" btnIsNext="false" @onClick="toPrevStep"/>
            </div>
            <Button btnTitle="Готово" btnIsNext="true" @onClick="toFinish"/>
          </div>
        </section>
        <!-- end of resultsContainer -->
      </div>
      <!-- end of step 2 -->
    </form>
  </div>
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
        name: '',
        surname: '',
        birthDate: null,
        citizenship: null,
        entryCountry: null,
        visaType: null,
        entryDate: null,
        departDate: null,
        try: null,
        timespent: null,
        cost: '€0'
      },
      isSecondStep: false,
      firstStepIsValid: false,
      secStepIsValid: false
    }
  },
  methods: {
    filterOptions (array) {
      const country = this.collectedInfo.entryCountry ? this.collectedInfo.entryCountry.id : 'RU'
      const filteredArr = array.filter(item => item.relative === country)
      return filteredArr
    },
    getCountrie (val) {
      this.collectedInfo.entryCountry = val
      this.collectedInfo.visaType = null
      this.collectedInfo.try = null
      this.collectedInfo.timespent = null
      this.calcSum()
    },
    getTypes (val) {
      this.collectedInfo.visaType = val
      this.calcSum()
    },
    getTry (val) {
      this.collectedInfo.try = val
      this.calcSum()
    },
    getTimespent (val) {
      this.collectedInfo.timespent = val
      this.calcSum()
    },
    getCitizenship (val) {
      this.collectedInfo.citizenship = val
    },
    getEntryDate (val) {
      this.collectedInfo.entryDate = val
    },
    getDepartDate (val) {
      this.collectedInfo.departDate = val
    },
    getBirthDate (val) {
      this.collectedInfo.birthDate = val
    },
    getName (val) {
      let newVal = val
      if (val) {
        val.trim()
        newVal = val[0].toUpperCase()
        newVal += val.slice(1).toLowerCase()
      }
      this.collectedInfo.name = newVal
    },
    getSurname (val) {
      let newVal = val
      if (val) {
        val.trim()
        newVal = val[0].toUpperCase()
        newVal += val.slice(1).toLowerCase()
      }
      this.collectedInfo.surname = newVal
    },
    calcSum () {
      let fullSum = 0
      if (this.collectedInfo.visaType) {
        fullSum += +this.collectedInfo.visaType.price.replace(/,/, '.')
      }
      if (this.collectedInfo.try) {
        fullSum += +this.collectedInfo.try.price.replace(/,/, '.')
      }
      if (this.collectedInfo.timespent) {
        fullSum += +this.collectedInfo.timespent.price.replace(/,/, '.')
      }
      this.collectedInfo.cost = '€' + fullSum
    },
    checkValid () {
      const firstStep = (
        this.collectedInfo.entryCountry &&
        this.collectedInfo.visaType &&
        this.collectedInfo.entryDate &&
        this.collectedInfo.departDate &&
        this.collectedInfo.try &&
        this.collectedInfo.timespent &&
        this.collectedInfo.cost !== '€0'
      )
      this.firstStepIsValid = firstStep

      const secStep = (
        this.firstStepIsValid &&
        this.collectedInfo.name &&
        this.collectedInfo.surname &&
        this.collectedInfo.birthDate &&
        this.collectedInfo.citizenship
      )
      this.secStepIsValid = secStep
    },
    toNextStep () {
      this.checkValid()
      if (this.firstStepIsValid) {
        this.isSecondStep = true
      } else {
        alert('Заполните все поля')
      }
    },
    toPrevStep () {
      this.isSecondStep = false
    },
    toFinish () {
      this.checkValid()
      if (this.secStepIsValid) {
        const data = {
          Имя: this.collectedInfo.name,
          Фамилия: this.collectedInfo.surname,
          'Дата рождения': this.collectedInfo.birthDate,
          Гражданство: this.collectedInfo.citizenship.name,
          'Страна въезда': this.collectedInfo.entryCountry.name,
          'Тип визы': this.collectedInfo.visaType.name,
          Въезд: this.collectedInfo.entryDate,
          Выезд: this.collectedInfo.departDate,
          'Количество заездов': this.collectedInfo.try.name,
          'Время обработки': this.collectedInfo.timespent.name,
          'Итоговая стоимость': this.collectedInfo.cost
        }
        console.log(JSON.stringify(data))
      } else {
        alert('Заполните все поля')
      }
    }
  },
  computed: {
    filteredTry () {
      return this.filterOptions(this.selectData.try)
    },
    filteredTimespent () {
      return this.filterOptions(this.selectData.timespent)
    },
    userName () {
      let name = 'Пользователь'
      if (this.collectedInfo.name) {
        name = this.collectedInfo.name
      }
      if (this.collectedInfo.surname) {
        name += ' ' + this.collectedInfo.surname[0].toUpperCase() + '.'
      }
      return name
    },
    minDate () {
      let min = ''
      if (this.collectedInfo.entryDate) {
        min = this.collectedInfo.entryDate
      }
      return min
    }
  }
}

</script>

<style lang="scss">
@import './applicForm.scss';
</style>
