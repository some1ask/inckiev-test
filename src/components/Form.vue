<template>
  <form action="" ref="myForm" @submit="checkForm">
    <div class="form__wrapper">
      <div class="form left-column">
        <p class="form__caption">Представьтесь, пожалуйста</p>
        <div class="form__item" :class="{ error: lastName.error !== null }">
          <label for="lastName">* Фамилия</label>
          <input id="lastName" type="text" v-model="lastName.value" />
          <span v-if="lastName.error">{{ lastName.error }}</span>
        </div>
        <div class="form__item" :class="{ error: name.error !== null }">
          <label for="name">* Имя</label>
          <input id="name" type="text" v-model="name.value" />
          <span v-if="name.error">{{ name.error }}</span>
        </div>
        <div class="form__item" :class="{ error: job.error !== null }">
          <label for="job">Организация и должность</label>
          <input id="job" type="text" v-model="job.value" />
          <span v-if="job.error">{{ job.error }}</span>
        </div>
        <div class="form__item radio__item">
          <input type="radio" name="radio" value="user" id="pick1" checked />
          <label for="pick1">Потребитель</label>
        </div>
        <div class="form__item radio__item">
          <input type="radio" name="radio" value="med" id="pick2" />
          <label for="pick2">Медицинский работник</label>
        </div>
        <div class="form__item radio__item">
          <input type="radio" name="radio" value="journalist" id="pick3" />
          <label for="pick3">Журналист</label>
        </div>
        <p class="form__caption">Сообщение</p>
        <div class="form__item" :class="{ error: subject.error !== null }">
          <label for="subject">Тема сообщения</label>
          <input id="subject" type="text" v-model="subject.value" />
          <span v-if="subject.error">{{ subject.error }}</span>
        </div>
        <div class="form__item" :class="{ error: message.error !== null }">
          <label for="message">* Сообщение</label>
          <textarea id="message" v-model="message.value"/>
           <span v-if="message.error">{{ message.error }}</span>
           
        </div>
      </div>
      <div class="form right-column">
        <p class="form__caption">Контактная информация</p>
        <div class="form__item" :class="{ error: email.error !== null }">
          <label for="email">* Email</label>
          <input id="email" type="text" v-model="email.value"/>
           <span v-if="email.error">{{ email.error }}</span>
        </div>
        <div class="form__item" :class="{ error: country.error !== null }">
          <label for="country">Страна</label>
          <input id="country" type="text" v-model="country.value" />
          <span v-if="country.error">{{ country.error }}</span>
        </div>
        <div class="form__item" :class="{ error: city.error !== null }">
          <label for="city">Город</label>
          <input id="city" type="text" v-model="city.value" />
          <span v-if="city.error">{{ city.error }}</span>
        </div>
        <div class="form__item" :class="{ error: zipCode.error !== null }">
          <label for="zipCode">Индекс</label>
          <input id="zipCode" type="text" v-model="zipCode.value" />
          <span v-if="zipCode.error">{{ zipCode.error }}</span>
        </div>
        <div class="form__item" :class="{ error: address.error !== null }">
          <label for="address">Адрес</label>
          <input id="address" type="text" v-model="address.value" />
          <span v-if="address.error">{{ address.error }}</span>
        </div>
        <div class="form__item" :class="{ error: phone.error !== null }">
          <label for="phone">* Телефон</label>
          <input
            id="phone"
            type="text"
            placeholder="(___)___-__-__"
            maxlength="14"
          v-model="phone.value" />
          <span v-if="phone.error">{{ phone.error }}</span>
          <span id="phoneLines"></span>
        </div>
        <div class="form__item">
          <input id="send" type="submit" value="отправить" />
        </div>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: {
        value: "",
        error: null,
        
      },
      lastName: {
        value: "",
        error: null,
        
      },
      job: {
        value: "",
        error: null,
        
      },
      subject: {
        value: "",
        error: null,
        
      },
      message: {
        value: "",
        error: null,
        
      },
      email: {
        value: "",
        error: null,
        
      },
      country: {
        value: "",
        error: null,
        
      },
      city: {
        value: "",
        error: null,
        
      },
      zipCode: {
        value: "",
        error: null,
        
      },
      address: {
        value: "",
        error: null,
        
      },
      phone: {
        value: "",
        error: null,
        
      },
    };
  },
  computed: {},
  methods: {
    checkCyrillic(obj) {
      if (/[А-Яа-яёЁ]+$/.test(obj.value)) {
        obj.error = null;
        
        return false;
      } else if (obj.value.length === 0) {
        obj.error = "Поле пустое";
        
        return true;
      } else {
        obj.error = "Только кирилицца";
        
        return true;
      }
    },
    checkEmail(obj) {
      if (/[A-Za-z0-9]+@[a-z]+\.[a-z]{2,3}$/.test(obj.value)) {
        console.log(obj);
        obj.error = null;
        
     
        return false;
      } else if (obj.value.length === 0) {
        obj.error = "Поле пустое";
        
           return true;
      } else {
        obj.error = "Пожалуйста введите формат емейла xxx@xxx.xxx";
        
          return true;
      }
    },
    checkNumbers(obj){
 if (/\d/.test(obj.value)) {
        obj.error = null;
        
        return false;
      } else if (obj.value.length === 0) {
        obj.error = "Поле пустое";
        
        return true;
      } else {
        obj.error = "Только цифры";
        
        return true;
      }
    },
    checkAddress(obj){
      if (/^[А-Яа-я\d\s,'.'/]+$/.test(obj.value)) {
        obj.error = null;
        
      return false;
      } else if (obj.value.length === 0) {
        obj.error = "Поле пустое";
        
        return true;
      } else {
        obj.error = "Только Кирилица цифры и символы ',', '/', '.'";
        
        return true;
      }
    },
    checkPhoneNumber(obj){
      console.log(obj)
 if (/\(\d{3}\)\d{3}-\d{2}-\d{2}/.test(obj.value)) {
        obj.error = null;
        
        return false;
      } else if (obj.value.length === 0) {
        obj.error = "Поле пустое";
        
        return true;
      } else {
        obj.error = "Пожалуйста введите формат мобильного телефона (ххх)ххх-хх-хх";
        
        return true;
      }
      
    },
    checkCyrillicAndNumbers(obj) {
      if (/^[а-яА-ЯёЁ0-9\s]+$/.test(obj.value)) {
        obj.error = null;
        

        return false;
      } else if (obj.value.length === 0) {
        obj.error = "Поле пустое";
        
        return true;
      } else {
        obj.error = "Только кирилицца";
        
                return true;
      }
    },
    checkForm: function (e) {
          
      e.preventDefault();
      
      const errors =[
      this.checkCyrillic(this.lastName),
      this.checkCyrillic(this.name),
      this.checkCyrillic(this.job),
      this.checkCyrillicAndNumbers(this.subject),
      this.checkCyrillicAndNumbers(this.message),
      this.checkEmail(this.email),
      this.checkCyrillic(this.country),
      this.checkCyrillic(this.city),
      this.checkNumbers(this.zipCode),
      this.checkAddress(this.address),
      this.checkPhoneNumber(this.phone)
      ];
      if(errors.some(error=>error )){
        console.log("NOT VALIDATED");
         console.log(errors);
      }
      else{
        alert("Отправлено");
        console.log(errors);
       Object.keys(this.$data).forEach(element => {
        this.$data[element].error = null;
        this.$data[element].value = "";

       });
        this.$refs.myForm.reset();
      }
    }
  }
};
</script>

<style lang="scss" scoped>
#message {
  height: 85px;
}
.form {
  &__wrapper {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    margin: 0 auto;
    justify-content: space-around;
    margin: 20px auto;
    padding: 20px;
  }
  &.right-column {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  &__item {
    font-size: 12px;
    position: relative;
    margin-bottom: 8px;
    &.error {
      transition: all 0.3s ease-in-out;
      input[type="text"],
    input[type="email"],
    textarea {
        border: 1px solid red;
        transition: all 0.3s ease-in-out;
      }
      span {
        transition: all 0.3s ease-in-out;
        color: red;
        display: block;
        width: 245px;
      }
    }
    label {
      font-size: 12px;
      text-transform: uppercase;
    }
    input[type="radio"] {
      margin-right: 5px;
    }
    input[type="submit"] {
      width: 250px;
      height: 32px;
      background-color: #464646;
      text-align: center;
      font-size: 22px;
      color: #fff;
      border: 1px solid #000;
    }
    input[type="text"],
    input[type="email"],
    textarea {
      padding: 0 5px;
      display: block;
      width: 250px;
      height: 30px;
      border: 1px solid #000;
      transition: all 0.3s ease-in-out;
      &:focus {
        outline: none;
      }
    }
    textarea {
      resize: none;
    }
  }

  &__caption {
    font-weight: 400;
    margin: 30px 0;
    text-transform: uppercase;
    &:nth-of-type(2) {
      margin: 10px 0;
    }
  }
}
#phone::placeholder {
  color: #000;
}
#phoneLines {

  &::before,
  &::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 1px;
    background-color: #000;
  }
  &::before {
    top: 17px;
  }
  &::after {
    top: 40px;
  }
}
</style>
