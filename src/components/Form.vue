<template>
  <form action="" @submit="checkForm">
    <div class="form__wrapper">
      <div class="form left-column">
        <p class="form__caption">Представьтесь, пожалуйста</p>
        <div class="form__item" >
          <label for="surname">* Фамилия</label>
          <input id="surname" type="text" v-model="lastName.value" />
          <span v-if="lastName.error">{{
            lastName.error
          }}</span>
        </div>
        <div class="form__item" :class="{'error':name.error !== null}">
          <label for="name">* Имя</label>
          <input id="name" type="text" v-model="name.value" />
          <span v-if="name.error">{{
            name.error
          }}</span>
        </div>
        <div class="form__item">
          <label for="job">Организация и должность</label>
          <input id="job" type="text" />
        
          
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
        <div class="form__item">
          <label for="subject">Тема сообщения</label>
          <input id="subject" type="text" />
        </div>
        <div class="form__item">
          <label for="message">* Сообщение</label>
          <textarea id="message" />
        </div>
      </div>
      <div class="form right-column">
        <p class="form__caption">Контактная информация</p>
        <div class="form__item">
          <label for="email">* Email</label>
          <input id="email" type="text" />
        </div>
        <div class="form__item">
          <label for="country">Страна</label>
          <input id="country" type="text" />
        </div>
        <div class="form__item">
          <label for="city">Город</label>
          <input id="city" type="text" />
        </div>
        <div class="form__item">
          <label for="zipCode">Индекс</label>
          <input id="zipCode" type="text" />
        </div>
        <div class="form__item">
          <label for="address">Адрес</label>
          <input id="address" type="text" />
        </div>
        <div class="form__item">
          <label for="phone">* Телефон</label>
          <input
            id="phone"
            type="text"
            placeholder="(___) ___-__-__"
            maxlength="10"
          />
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
        value:"",
        error:null,
        isError:false
      },
      lastName: {
        value:"",
        error:null,
        isError:false
      },
      job: {
        value:"",
        error:null,
        isError:false
      },
      subject: {
        value:"",
        error:null,
        isError:false
      },
      message: {
        value:"",
        error:null,
        isError:false
      },
      email: {
        value:"",
        error:null,
        isError:false
      },
      country: {
        value:"",
        error:null,
        isError:false
      },
      city: {
        value:"",
        error:null,
        isError:false
      },
      zipCode: {
        value:"",
        error:null,
        isError:false
      },
      address: {
        value:"",
        error:null,
        isError:false
      },
      phone: {
        value:"",
        error:null,
        isError:false
      },  
    };
  },
 computed: {
   
  },
  methods: {
    checkCyrillic(obj) {
      if (/[А-я]/.test(obj.value)) {
        obj.error = null;
        obj.isError = false;
        return true;
      } else if(obj.value.length === 0) {
        obj.error = "Поле пустое"
        obj.isError = true;
        return false;
      } 
      else{
        obj.error = "Только кирилицца"
        obj.isError = true;
        return false;
      }
        
      },
    checkForm: function (e) {
      this.checkCyrillic(this.name);
      e.preventDefault();
    },
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
    &.error{
      border:1px solid red;
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
    &:focus {
      outline: none;
    }
  }
  textarea {
    resize: none;
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
