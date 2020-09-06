<template id="form-for-app">
<form class="app-form" @submit.prevent="checkForm">
<h1> Регистрация нового клиента </h1>

<!--
    Блок с личными данными, информацией о лечащем враче и т.д.
-->
<div class="block-personal-data">

    <h2> Личные данные </h2>

      <div class="block-personal-data__fio">

        <!-- Фамилия -->
          <p> <label for="lastname"> Фамилия* </label>
            <input
            id="lastname"
            type="text"
            v-model.trim="lastname"
            :class="{invalid: ($v.lastname.$dirty && !$v.lastname.required) || ($v.lastname.$dirty && !$v.lastname.alpha)}"></p>
        <!-- Вывод сообщений при ошибке -->
          <small class="helper-text invalid" v-if="$v.lastname.$dirty && !$v.lastname.required"> <p>Это поле обязательно для заполнения</p> </small>
          <small class="helper-text invalid" v-else-if="$v.lastname.$dirty && !$v.lastname.alpha"><p> Фамилия должна содержать только буквы</p> </small>

        <!-- Имя -->
          <p> <label for="firstname"> Имя* </label>
            <input id="firstname"
            type="text"
            v-model.trim="firstname"
            :class="{invalid: ($v.firstname.$dirty && !$v.firstname.required) || ($v.firstname.$dirty && !$v.firstname.alpha)}"> </p>
        <!-- Вывод сообщений при ошибке -->
          <small class="helper-text invalid" v-if="$v.firstname.$dirty && !$v.firstname.required"> Это поле обязательно для заполнения </small>
          <small class="helper-text invalid" v-else-if="$v.firstname.$dirty && !$v.firstname.alpha"> Имя должно содержать только буквы </small>

        <!-- Отчество -->
          <p> <label for="fathername"> Отчество </label>
            <input id="fathername"
            type="text"
            v-model.trim="fathername"
            :class="{invalid:  ($v.fathername.$dirty && !$v.fathername.alpha)}"> </p>
        <!-- Вывод сообщений при ошибке -->
          <small class="helper-text invalid" v-if="$v.fathername.$dirty && !$v.fathername.alpha"> Отчество должно содержать только буквы </small>
      </div>

        <!-- Дата рождения -->
          <p> <label for="birth"> Дата рождения* </label>
            <input id="birth"
            type="date"
            v-model.trim="birth"
            :class="{invalid: ($v.birth.$dirty && !$v.birth.required)}"> </p>
        <!-- Вывод сообщений при ошибке -->
          <small class="helper-text invalid" v-if="$v.birth.$dirty && !$v.birth.required"> Это поле обязательно для заполнения </small>
        <!-- Номер телефона -->
          <p> <label for="number"> Номер телефона* +</label>
            <input id="number"
            type="text"
            placeholder="79388785511"
            v-model.trim="number"
            :class="{invalid: ($v.number.$dirty && !$v.number.required) || ($v.number.$dirty && !$v.number.minLength) || ($v.number.$dirty && !$v.number.maxLength) || ($v.number.$dirty && !$v.number.alphaNum)}"> </p>
        <!-- Вывод сообщений при ошибке -->
          <small class="helper-text invalid" v-if="$v.number.$dirty && !$v.number.required"> Это поле обязательно для заполнения </small>
          <small class="helper-text invalid" v-else-if="($v.number.$dirty && !$v.number.minLength) || ($v.number.$dirty && !$v.number.maxLength)"> Номер телефона должен содержать 11 цифр </small>
          <small class="helper-text invalid" v-if="$v.number.$dirty && !$v.number.alphaNum"> <p> Номер телефона должен содержать только цифры </p> </small>

        <!-- Пол -->
          <p> <label for="pol"> Пол </label> M <input type="radio" name="pol" value="male"> Ж  <input type="radio" name="pol" value="female"></p>

        <!-- Группа клиентов -->
          <p> <label for="group"> Группа клиентов* </label>
            <select id="group" multiple
            v-model.trim="group"
            :class="{invalid: ($v.group.$dirty && !$v.group.required)}"
            size="1" onmouseout="this.size='1';" onmouseover="this.size='3';"  clients = "clients[]">
              <option value="vip"> VIP </option>
              <option value="trouble"> Проблемные </option>
              <option value="oms"> ОМС </option>
            </select> </p>
        <!-- Вывод сообщений при ошибке -->
          <small class="helper-text invalid" v-if="$v.group.$dirty && !$v.group.required"> Пожалуйста, выберите одну из групп </small>

        <!-- Лечащий врач -->
          <p> <label for="doctor"> Лечащий врач </label>
            <select>
              <option></option>
              <option>Иванов</option>
              <option>Захаров</option>
              <option>Чернышева</option>
            </select></p>

        <!-- Отправлять смс или нет -->
          <p> <label for="sms"> Не отправлять смс </label> <input type="checkbox" name="sms" value="true"> </p>
        </div>


  <!--
      Блок с информацией о месте проживания
  -->

<div class="block-info-about-address">

    <h2> Адрес </h2>

  <!-- Индекс -->
     <p> <label for="index"> Индекс </label>
       <input id="index"
       type="text"
       v-model.trim="index"
       :class="{invalid: ($v.index.$dirty && !$v.index.alphaNum) }"
       > </p>
       <!-- Вывод сообщений при ошибке -->
       <small class="helper-text invalid" v-if="$v.index.$dirty && !$v.index.alphaNum"> Индекс должен состоять только из цифр </small>

  <!-- Страна -->
      <p> <label for="country"> Страна </label>
        <input id="country"
        type="text"
        v-model.trim="country"
        :class="{invalid: ($v.country.$dirty && !$v.country.alpha) }"> </p>
    <!-- Вывод сообщений при ошибке -->
      <small class="helper-text invalid" v-if="$v.country.$dirty && !$v.country.alpha"> Название страны должно состоять только из букв </small>

  <!-- Область -->
      <p> <label for="district"> Область </label>
          <input id="district"
          type="text"
          v-model.trim="district"
          :class="{invalid: ($v.district.$dirty && !$v.district.alpha) }"> </p>
    <!-- Вывод сообщений при ошибке -->
      <small class="helper-text invalid" v-if="$v.district.$dirty && !$v.district.alpha"> Название области должно состоять только из букв </small>

  <!-- Город -->
      <p> <label for="city"> Город* </label>
          <input id="city"
          type="text"
          v-model.trim="city"
          :class="{invalid: ($v.city.$dirty && !$v.city.alpha) || ($v.city.$dirty && !$v.city.required)}"> </p>
    <!-- Вывод сообщений при ошибке -->
      <small class="helper-text invalid" v-if="$v.city.$dirty && !$v.city.alpha"> Название города должно состоять только из букв </small>
      <small class="helper-text invalid" v-else-if="$v.city.$dirty && !$v.city.required"> Это поле обязательно для заполнения </small>

  <!-- Улица -->
      <p> <label for="street"> Улица </label>
        <input id="street"
        type="text"> </p>

  <!-- Дом -->
      <p> <label for="house"> Дом </label> <input id="house" type="text"> </p>

</div>

  <!--
      Блок с паспортными данными
  -->

<div class="block-passport-data">

  <h2> Паспортные данные </h2>

  <!-- Тип документа -->
    <p> <label for="typedoc"> Тип документа* </label>
      <select id="typedoc"
      v-model.trim="typedoc"
      :class="{invalid: ($v.typedoc.$dirty && !$v.typedoc.required)}">
        <option>Паспорт</option>
        <option>Свидетельство о рождении</option>
        <option>Водительское удостоверение</option>
      </select></p>
  <!-- Вывод сообщений при ошибке -->
    <small class="helper-text invalid" v-if="$v.typedoc.$dirty && !$v.typedoc.required"> Пожалуйста, выберите тип документа </small>

  <!-- Серия паспорта -->
      <p> <label for="seriapassport"> Серия </label>
          <input id="seriapassport"
          type="text"
          v-model.trim="seriapassport"
          :class="{invalid:  ($v.seriapassport.$dirty && !$v.seriapassport.minLength) || ($v.seriapassport.$dirty && !$v.seriapassport.maxLength) || ($v.seriapassport.$dirty && !$v.seriapassport.alphaNum)}"
          > </p>
  <!-- Вывод сообщений при ошибке -->
    <small class="helper-text invalid" v-if="($v.seriapassport.$dirty && !$v.seriapassport.minLength) || ($v.seriapassport.$dirty && !$v.seriapassport.maxLength)"> Серия паспорта должна содержать 4 цифры </small>
    <small class="helper-text invalid" v-else-if="$v.seriapassport.$dirty && !$v.seriapassport.alphaNum"> <p> Серия паспорта должна содержать только цифры </p> </small>

<!-- Номер паспорта -->
      <p> <label for="numpassport"> Номер </label>
          <input id="numpassport"
           type="text"
           v-model.trim="numpassport"
           :class="{invalid:  ($v.numpassport.$dirty && !$v.numpassport.minLength) || ($v.numpassport.$dirty && !$v.numpassport.maxLength) || ($v.numpassport.$dirty && !$v.numpassport.alphaNum)}"
           > </p>
  <!-- Вывод сообщений при ошибке -->
      <small class="helper-text invalid" v-if="($v.numpassport.$dirty && !$v.numpassport.minLength) || ($v.numpassport.$dirty && !$v.numpassport.maxLength)"> Номер паспорта должен содержать 6 цифр </small>
      <small class="helper-text invalid" v-else-if="$v.numpassport.$dirty && !$v.numpassport.alphaNum"> <p> Номер паспорта должен содержать только цифры </p> </small>

  <!-- Кем выдан  -->
      <p> <label for="issued-passport"> Кем выдан паспорт </label> <input id="issued-passport" type="text"> </p>

  <!-- Дата выдачи  -->
      <p> <label for="datepassport"> Дата выдачи* </label>
          <input id="datepassport"
          type="date" v-model.trim="datepassport"
           :class="{invalid: ($v.datepassport.$dirty && !$v.datepassport.required) || ($v.datepassport.$dirty && !$v.datepassport.validDate)}"> </p>
    <!-- Вывод сообщений при ошибке -->
      <small class="helper-text invalid" v-if="$v.datepassport.$dirty && !$v.datepassport.required"> Это поле обязательно для заполнения </small>

</div>

<!-- Кнопка создания клиента -->
    <p><button type="submit" class="btn-for-submit" v-on:click="success"> Создать </button> </p>
</form>
</template>

<script>
  import {minLength, maxLength, alpha, alphaNum, required} from 'vuelidate/lib/validators'
  export default {
    name: 'Form',
    data:() =>  ({
      lastname: '',
      firstname: '',
      fathername:'',
      birth: '',
      number:'7',
      group:[],
      index:'',
      country:'',
      district:'',
      city:'',
      typedoc:'',
      seriapassport:'',
      numpassport:'',
      datepassport:''
    }),
    validations: {
      lastname: {required, alpha: val => /^[а-яё]*$/i.test(val)},
      firstname: {required, alpha: val => /^[а-яё]*$/i.test(val)},
      fathername: {alpha: val => /^[а-яё]*$/i.test(val)},
      birth: {required},
      number: {required, minLength: minLength(11), maxLength: maxLength(11), alphaNum: val => /^[0-9]*$/i.test(val)},
      group: {required},
      index:{alphaNum},
      country:{alpha},
      district:{alpha},
      city:{alpha: val => /^[а-яё]*$/i.test(val), required},
      typedoc:{required},
      seriapassport:{minLength: minLength(4), maxLength: maxLength(4), alphaNum: val => /^[0-9]*$/i.test(val)},
      numpassport:{minLength: minLength(6), maxLength: maxLength(6), alphaNum: val => /^[0-9]*$/i.test(val)},
      datepassport:{required}
    },
    methods: {
      checkForm() {
        if (this.$v.$invalid){
          this.$v.$touch()
          return
        }
      },
      success: function () {
        if (!this.$v.$invalid){
          alert('Поздравляем! Регистрация прошла успешно!');
        }
    }
  }
}
</script>

<style lang="scss">

$color-almost-white: #f4f4f4;
$color-light-green: #1fd187;
$color-dark-green: #19c27c;
$color-red: #fa2f2f;

@media screen and (min-width: 768px) and (max-width: 991px){
  .app-form{
      font-size: 90%;
  }
}
@media screen and (max-width: 767px){
  .app-form{
    font-size: 80%;
  }
  #app .block-personal-data{
    width: 100%;
  }
  #app p{
    margin: 15px 0 0 0;
  }
  #app .block-info-about-address{
    width: 100%;
  }
  #app .block-passport-data{
    width: 100%;
  }
  #app input[type=text]{
    display: block;
    text-align: center;
    width: 80%;
    margin: 0 auto;
  }
}

.app-form{
  width: 80%;
  margin: 0 auto;
}
.app-form input[type=text], input[type=date]{
  border-radius: 8px;
  height: 20px;
  width: 200px;
}
/*Стили для личных данных*/
.block-personal-data{
    background-color: $color-almost-white;
    padding-top: 50px;
    padding-bottom: 50px;
    width: 70%;
    margin: 0 auto;
    border: 1px solid $color-light-green;
    border-radius: 15px;
    margin-bottom: 50px;
}
.block-personal-data h2{
  padding-bottom: 20px;
}
.block-personal-data p{
    margin-left: 20px;
    margin-top: 20px;
}
#group{
  border-radius: 8px;
  height: 50px;
  width: 200px;
}
/*Изменение цвета вспомогательного текста*/
.helper-text{
    color: $color-red;
    width: 300px;
}
/*Стили для адреса*/
.block-info-about-address{
    background-color: $color-almost-white;
    padding-top: 50px;
    padding-bottom: 50px;
    width: 70%;
    margin: 0 auto;
    border: 1px solid $color-light-green;
    border-radius: 15px;
    margin-bottom: 50px;
}
.block-info-about-address p{
  margin-left: 20px;
  margin-top: 20px;
}
/*Стили для паспортных данных*/
.block-passport-data{
    background-color: $color-almost-white;
    padding-top: 50px;
    padding-bottom: 50px;
    width: 70%;
    margin: 0 auto;
    border: 1px solid $color-light-green;
    border-radius: 15px;
}
.block-passport-data p{
  margin-left: 20px;
  margin-top: 20px;
}
/*Стилизация кнопки*/
.btn-for-submit{
  border-radius: 20px;
  height: 40px;
  width: 180px;
  color: white;
  background-color: $color-light-green;
  border: none;
  font-size: 0.9em;
}
.btn-for-submit:hover{
  background-color: $color-dark-green;
}
</style>
