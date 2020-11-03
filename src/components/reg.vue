<template>
 <div class="main_form">
    <div v-if="$v.form.$error">
      ERROR
    </div>
    <form @submit.prevent="onSubmit">
      <div class="form__group field">
        <input v-model="form.surname" type="input" class="form__field" placeholder="suname" name="suname" id='suname' />
        <label for="suname" class="form__label">Suname*</label>
      </div>
      <div class="form__group field">
        <input v-model="form.name" type="input" class="form__field" placeholder="Name" name="Name" id='Name' />
        <label for="name" class="form__label">Name*</label>
      </div>
      <div class="form__group field">
        <input v-model="form.patronymic" autocomplete="off" type="input" class="form__field" placeholder="patronymic" name="patronymic" id='patronymic' />
        <label for="patronymic" class="form__label">Patronymic</label>
      </div>
      <div class="form__group field">
        <input v-model="form.date" autocomplete="off" type="date" class="form__field" placeholder="Date" name="date" id='date' />
        <label for="date" class="form__label">Date*</label>
      </div>
      <div class="form__group field">
        <input @keypress="isNumber($event)" v-on:click="Numb7" v-model="form.numb" autocomplete="off" type="input" class="form__field" placeholder="numb" name="numb" id='numb' />
        <label for="numb" class="form__label">Number*</label>
      </div>
      <div class="form__group field">
          <label class="form__field">
              <span>Sex:</span>
          </label>
          <label class="radio" >
              <input type="radio" name="r"  value="1" @change="form.male = true">
              <span>Male</span>
          </label>
          <label class="radio">
              <input type="radio" name="r"  value="2" @change="form.male = false">
              <span>Female</span>
          </label>
      </div>
      <div class="form__group field">
        <label class="form__field">
              <span>Group clients*:</span>
        </label>

        <label class="container">VIP
          <input value="VIP" v-model="form.checkedGroup" type="checkbox">
          <span class="checkmark"></span>
        </label>

        <label class="container">Проблемные
          <input value="Проблемные" v-model="form.checkedGroup" type="checkbox">
          <span class="checkmark"></span>
        </label>

        <label class="container">ОМС
          <input value="ОМС" v-model="form.checkedGroup" type="checkbox">
          <span class="checkmark"></span>
        </label>
      </div>
      <div class="form__group field">
        <label class="form__field">
              <span>Attending doctor: </span>
        </label>
        <select v-model="selected">
        <option disabled value="">Выберите один из вариантов</option>
        <option>Иванов</option>
        <option>Захаров</option>
        <option>Чернышева</option>
      </select>
      </div>
      <div class="form__group field">
        <label class="container"> Не Отправлять СМС
          <input type="checkbox" v-model="form.NotSendSMS" checked="checked">
          <span class="checkmark"></span>
        </label>
      </div>
      <br>
      <div class="form__group field">
       <button class="SubBut" type="submit"> Submit </button>
      </div>
    </form>
 </div>
</template>

<script>
import { required, minLength, maxLength } from 'vuelidate/lib/validators'
export default {
  data () {
    return {
      form: {
        surname: '',
        name: '',
        patronymic: '',
        date: '',
        numb: '',
        male: false,
        checkedGroup: [],
        doctor: '',
        NotSendSMS: true
      }
    }
  },
  validations: {
    form: {
      surname: { required, min: minLength(3) },
      name: { required, min: minLength(3) },
      date: { required, min: minLength(10), max: maxLength(10) },
      numb: { required, min: minLength(10), max: maxLength(11) },
      checkedGroup: { required }
    }
  },
  methods: {
    ValidDate () {
      console.log(this.form.date.length)
      if (this.form.date.length === 2) {
        this.form.date += '.'
      }
      if (this.form.date.length === 5) {
        this.form.date += '.'
      }
    },
    isNumber (evt) {
      var charCode = (evt.which) ? evt.which : evt.keyCode
      if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
        evt.preventDefault()
      } else {
        return true
      }
    },
    ValidNumb () {
      console.log(this.form.numb.length)
    },
    Numb7 () {
      if (this.form.numb.length === 0) {
        this.form.numb += '+7'
      }
    },
    onSubmit () {
      this.$v.form.$touch()
    }
  }
}
</script>
