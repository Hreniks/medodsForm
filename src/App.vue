<template>
  <div id="app">
    <section class="form">
      <div class="container">
        <h1 class="form__title">Регистрация</h1>
        <form class="reg-form" action="" @submit.prevent="submit" novalidate>
          <small class="reg-form__small"
            >*Поле обязательное для заполнения.</small
          >

          <div class="reg-form__surname">
            <label class="reg-form__label" for="surname">Фамилия<span style="color: red">*</span></label>
            <input
              class="reg-form__input"
              placeholder="Фамилия*"
              id="surname"
              type="text"
              v-model.trim="surname"
              :class="{
                'reg-form__input--invalid': $v.surname.$error,
              }"
            />
          </div>
          <div class="error">
            <small class="error__message" v-if="!$v.surname.required && $v.surname.$dirty"
              >Поле Фамилия является обязательным</small
            >
        
          </div>

          

          <div class="reg-form__name">
            <label class="reg-form__label" for="name">Имя<span style="color: red">*</span></label>
            <input
              class="reg-form__input"
              placeholder="Имя*"
              id="name"
              type="text"
              v-model.trim="name"
              :class="{
                'reg-form__input--invalid': $v.surname.$error,
              }"
            />
          </div>
          <div class="error">
            <small class="error__message" v-if="!$v.name.required && $v.name.$dirty"
              >Поле Имя является обязательным</small
            >
            
          </div>


          <div class="reg-form__patronymic">
            <label class="reg-form__label" for="patronymic">Отчество</label>
            <input
              class="reg-form__input"
              placeholder="Отчество"
              id="patronymic"
              type="text"
            />
          </div>

          <div class="reg-form__date">
            <label class="reg-form__label" for="date">Дата рождения<span style="color: red">*</span></label>
            <input
              class="reg-form__input"
              placeholder="Дата рождения*"
              id="date"
              type="date"
              v-model.trim="date"
              :class="{
                'reg-form__input--invalid': $v.date.$error,
              }"
            />
          </div>
          <div class="error">
            <small class="error__message" v-if="$v.date.$error"
              >Поле Дата является обязательным</small
            >
          </div>

          <div class="reg-form__phone">
            <label class="reg-form__label" for="phone">Номер телефона<span style="color: red">*</span></label>
            <input
              class="reg-form__input"
              placeholder="Номер телефона*"
              id="phone"
              type="tel"
              v-model.trim="phone"
              @input="onlyNumbers"
              :class="{
                'reg-form__input--invalid': $v.phone.$error,
              }"
            />
          </div>
          <div class="error">
            <small class="error__message" v-if="$v.phone.$error"
              >Введите корректный номер телефона</small
            >
          </div>

          <div class="reg-form__gender">
            <label class="reg-form__label">Ваш пол:</label>
            <label
              class="reg-form__label reg-form__gender__label--male"
              for="male"
              >Мужской</label
            >
            <input
              class="reg-form__input"
              placeholder=""
              id="male"
              type="checkbox"
            />
            <label
              class="reg-form__label reg-form__gender__label--female"
              for="female"
              >Женский</label
            >
            <input
              class="reg-form__input"
              placeholder=""
              id="female"
              type="checkbox"
            />
          </div>

          <div class="reg-form__client-group">
            <label class="reg-form__label">Группа клиентов<span style="color: red">*</span></label>
            <select
              class="reg-form__select"
              multiple
              v-model.trim="status"
              :class="{ 'reg-form__select--invalid': $v.status.$error }"
            >
              <option
                class="reg-form__select-option"
                v-for="(client, i) in clientItems"
                :key="i"
                :value="client"
              >
                {{ client }}
              </option>
            </select>
          </div>

          <div class="error">
            <small class="error__message" v-if="$v.status.$error"
              >Выберите группу клиентов</small
            >
          </div>

          <div class="reg-form__doctor">
            <label class="reg-form__label" for="doctor">Лечащий врач</label>
            <select class="reg-form__select" name="" id="doctor">
              <option v-for="(doctor, i) in doctors" :key="i" :value="doctor">
                {{ doctor }}
              </option>
            </select>
          </div>

          <div class="reg-form__no-sms">
            <label class="reg-form__label" for="no-sms"
              >Не отправлять СМС</label
            >
            <input
              class="reg-form__input"
              placeholder=""
              id="no-sms"
              type="checkbox"
            />
          </div>

          <h1 class="form__title form__title--form">Адрес</h1>

          <div class="reg-form__index">
            <label class="reg-form__label" for="index">Индекс</label>
            <input
              class="reg-form__input"
              placeholder="Индекс"
              id="index"
              type="text"
            />
          </div>

          <div class="reg-form__country">
            <label class="reg-form__label" for="country">Страна</label>
            <input
              class="reg-form__input"
              placeholder="Страна"
              id="country"
              type="text"
            />
          </div>

          <div class="reg-form__region">
            <label class="reg-form__label" for="region">Область</label>
            <input
              class="reg-form__input"
              placeholder="Область"
              id="region"
              type="text"
            />
          </div>

          <div class="reg-form__city">
            <label class="reg-form__label" for="city">Город<span style="color: red">*</span></label>
            <input
              class="reg-form__input"
              placeholder="Город*"
              id="city"
              type="text"
              v-model.trim="city"
              :class="{
                'reg-form__input--invalid': $v.city.$error,
              }"
            />
          </div>

          <div class="error">
            <small class="error__message" v-if="!$v.city.required && $v.city.$dirty"
              >Поле Город является обязательным</small
            >
          </div>

          <div class="reg-form__street">
            <label class="reg-form__label" for="street">Улица</label>
            <input
              class="reg-form__input"
              placeholder="Улица"
              id="street"
              type="text"
            />
          </div>

          <div class="reg-form__house">
            <label class="reg-form__label" for="house">Дом</label>
            <input
              class="reg-form__input"
              placeholder="Дом"
              id="house"
              type="text"
            />
          </div>

          <h1 class="form__title form__title--form">Паспорт</h1>

          <div class="reg-form__type">
            <label class="reg-form__label" for="type">Тип документа<span style="color: red">*</span></label>
            <select
              class="reg-form__select"
              name=""
              id="type"
              v-model.trim="document"
              :class="{
                'reg-form__select--invalid': $v.document.$error,
              }"
            >
              <option v-for="(doc, i) in docType" :key="i" :value="doc">
                {{ doc }}
              </option>
            </select>
          </div>

          <div class="error">
            <small class="error__message" v-if="$v.document.$error"
              >Выберите тип документа</small
            >
          </div>

          <div class="reg-form__series">
            <label class="reg-form__label" for="series">Серия</label>
            <input
              class="reg-form__input"
              placeholder="Серия"
              id="series"
              type="text"
            />
          </div>

          <div class="reg-form__number">
            <label class="reg-form__label" for="number">Номер</label>
            <input
              class="reg-form__input"
              placeholder="Номер"
              id="number"
              type="text"
            />
          </div>
          <div class="reg-form__issued">
            <label class="reg-form__label" for="issued">Кем выдан</label>
            <input
              class="reg-form__input"
              placeholder="Кем выдан"
              id="issued"
              type="text"
            />
          </div>

          <div class="reg-form__date-out">
            <label class="reg-form__label" for="date-out">Дата выдачи<span style="color: red">*</span></label>
            <input
              class="reg-form__input"
              placeholder=""
              id="date-out"
              v-model.trim="dateOut"
              type="date"
              :class="{
                'reg-form__input--invalid': $v.dateOut.$error,
              }"
            />
          </div>
          <div class="error">
            <small class="error__message" v-if="$v.dateOut.$error"
              >Выберите дату выдачи</small
            >
          </div>

          <button class="reg-form__submit" type="submit">
            Завершить регистрацию
          </button>
        </form>
        <Done
          v-model="showPopup"
          v-if="showPopup"
          @click="showPopup = true"
          @close="showPopup = false"
        />
      </div>
    </section>
  </div>
</template>

<script>
import {
  required,
  maxLength,
  minLength,
  minValue,
  numeric
} from "vuelidate/lib/validators";
import Done from "@/components/done";

export default {
  name: "App",
  data() {
    return {
      surname: "",
      name: "",
      date: "",
      phone: "7",
      clientItems: ["VIP", "Проблемные", "ОМС"],
      status: [],
      doctors: ["Иванов", "Захаров", "Чернышева"],
      city: "",
      document: "",
      docType: ["Паспорт", "Свидетельство о рождении", "Вод. удостоверение"],
      dateOut: "",
      showPopup: false,
    };
  },
  components: {
    Done,
  },
  methods: {
    onlyNumbers() {
      this.phone = this.phone.replace(/[^+0-9]/gi, "");
    },
    submit() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      } else this.showPopup = true;
    },
  },
  validations: {
    name: {
      required,
     
    },
    surname: {
      required,
      
    },
    date: {
      required,
    },
    phone: {
      required,
      maxLength: maxLength(11),
      minLength: minLength(11),
      numeric
    },
    status: {
      required,
    },
    city: {
      required,
    },
    document: {
      required,
    },
    dateOut: {
      required,
      minValue,
    },
  },
};
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  padding: 5rem 0;
}
</style>
