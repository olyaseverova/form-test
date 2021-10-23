<template>
  <div class="form">
    <h1 class="headline">Регистрация</h1>
    <section class="account">
      <p>Уже есть аккаунт?</p>
      <router-link class="link" to="#">Войти</router-link>
    </section>
    <form class="sign-up" method="post" action="" enctype="multipart/form-data">
      <section class="sign-up__questions">
        <label class="sign-up__label">
          <p class="sign-up__p">Имя</p>
          <input
            class="sign-up__input sign-up__name"
            type="text"
            pattern="^[А-Яа-яЁё\s-]+$"
            placeholder="Введите Ваше имя"
            @click="checkName"
            @keyup="checkName"
          />
        </label>
        <label class="sign-up__label">
          <p class="sign-up__p">Еmail</p>
          <input
            class="sign-up__input sign-up__email"
            type="email"
            placeholder="Введите ваш email"
            pattern="^[^@\s]+@[^@\s]+\.[^@\s]+$"
            @click="checkEmail"
            @keyup="checkEmail"
          />
        </label>
        <label class="sign-up__label">
          <p class="sign-up__p">Номер телефона</p>
          <input
            class="sign-up__input sign-up__tel"
            type="tel"
            placeholder="Введите номер телефона"
            minlength="12"
            maxlength="18"
            @click="checkTel"
            @keyup="checkTel"
            pattern="\+?\d{1,4}?[-.\s]?\(?\d{1,3}?\)?[-.\s]?\d{1,4}[-.\s]?\d{1,4}[-.\s]?"
          />
        </label>
        <label class="sign-up__label sign-up__language">
          <p class="sign-up__p">Язык</p>
          <ul class="languages-list list">
            <li
              class="languages-list__item none"
              v-for="language in languages"
              :class="{ language_shown: language.checked }"
              :key="language.id"
              :id="language.id"
            >
              <label class="languages-list__label" :id="language.id">
                <input
                  class="languages-list__input visually-hidden"
                  type="radio"
                  name="language"
                  :checked="language.checked"
                  :class="{ language_input_shown: language.checked }"
                  :id="language.id"
                  @click="activateLanguages"
                  @focus="focusLanguages"
                />
                <p class="languages-list__text" :id="language.id">
                  {{ language.title }}
                </p>
              </label>
            </li>
          </ul>
        </label>
      </section>
      <input
        class="conditions-input visually-hidden"
        type="checkbox"
        id="condition"
      />
      <label class="conditions-label" for="condition" @click="checkConditions">
        <p class="conditions-text">Принимаю</p>
        <router-link class="link" to="#">условия</router-link>
        <p class="conditions-text">использования</p>
      </label>
      <button class="sign-up__button" type="submit" disabled>
        Зарегистрироваться
      </button>
    </form>
  </div>
</template>

<script>
export default {
  methods: {
    activateLanguages: function (event) {
      let languageItems = document.querySelectorAll(".languages-list__item");
      languageItems.forEach(function (language) {
        language.classList.toggle("none");
        if (event.target.id === language.id) {
          if (event.target.classList.contains("language_input_shown")) {
            language.classList.remove("language_shown");
            event.target.classList.remove("language_input_shown");
          } else {
            language.classList.add("language_shown");
            event.target.classList.add("language_input_shown");
          }
        }
      });
    },

    focusLanguages: function () {
      let nameInput = document.querySelector(".sign-up__name");
      let emailInput = document.querySelector(".sign-up__email");
      let telInput = document.querySelector(".sign-up__tel");
      if (nameInput.textLength < 1) {
        nameInput.setAttribute("required", "required");
      }
      if (emailInput.textLength < 1) {
        emailInput.setAttribute("required", "required");
      }
      if (telInput.textLength < 1) {
        telInput.setAttribute("required", "required");
      }
    },

    checkTel: function () {
      let inputElement = document.querySelector(".conditions-input");
      let buttonElement = document.querySelector(".sign-up__button");
      let nameInput = document.querySelector(".sign-up__name");
      let emailInput = document.querySelector(".sign-up__email");
      let telInput = document.querySelector(".sign-up__tel");

      if (nameInput.textLength < 1) {
        nameInput.setAttribute("required", "required");
      }
      if (emailInput.textLength < 1) {
        emailInput.setAttribute("required", "required");
      }

      if (
        inputElement.classList.contains("conditions-input-checked") &&
        nameInput.value.search(/^[А-Яа-яЁё\s-]+$/) === 0 &&
        emailInput.value.search(/^[^@\s]+@[^@\s]+\.[^@\s]+$/) === 0 &&
        telInput.value.search(
          /\+?\d{1,4}?[-.\s]?\(?\d{1,3}?\)?[-.\s]?\d{1,4}[-.\s]?\d{1,4}[-.\s]?/
        ) === 0
      ) {
        buttonElement.disabled = false;
      } else {
        buttonElement.disabled = true;
      }
    },

    checkEmail: function () {
      let inputElement = document.querySelector(".conditions-input");
      let buttonElement = document.querySelector(".sign-up__button");
      let nameInput = document.querySelector(".sign-up__name");
      let emailInput = document.querySelector(".sign-up__email");
      let telInput = document.querySelector(".sign-up__tel");

      if (nameInput.textLength < 1) {
        nameInput.setAttribute("required", "required");
      }

      if (
        inputElement.classList.contains("conditions-input-checked") &&
        nameInput.value.search(/^[А-Яа-яЁё\s-]+$/) === 0 &&
        emailInput.value.search(/^[^@\s]+@[^@\s]+\.[^@\s]+$/) === 0 &&
        telInput.value.search(
          /\+?\d{1,4}?[-.\s]?\(?\d{1,3}?\)?[-.\s]?\d{1,4}[-.\s]?\d{1,4}[-.\s]?/
        ) === 0
      ) {
        buttonElement.disabled = false;
      } else {
        buttonElement.disabled = true;
      }
    },

    checkName: function () {
      let inputElement = document.querySelector(".conditions-input");
      let buttonElement = document.querySelector(".sign-up__button");
      let nameInput = document.querySelector(".sign-up__name");
      let emailInput = document.querySelector(".sign-up__email");
      let telInput = document.querySelector(".sign-up__tel");

      if (
        inputElement.classList.contains("conditions-input-checked") &&
        nameInput.value.search(/^[А-Яа-яЁё\s-]+$/) === 0 &&
        emailInput.value.search(/^[^@\s]+@[^@\s]+\.[^@\s]+$/) === 0 &&
        telInput.value.search(
          /\+?\d{1,4}?[-.\s]?\(?\d{1,3}?\)?[-.\s]?\d{1,4}[-.\s]?\d{1,4}[-.\s]?/
        ) === 0
      ) {
        buttonElement.disabled = false;
      } else {
        buttonElement.disabled = true;
      }
    },

    checkConditions: function () {
      let inputElement = document.querySelector(".conditions-input");
      let buttonElement = document.querySelector(".sign-up__button");
      let nameInput = document.querySelector(".sign-up__name");
      let emailInput = document.querySelector(".sign-up__email");
      let telInput = document.querySelector(".sign-up__tel");
      if (nameInput.textLength < 1) {
        nameInput.setAttribute("required", "required");
      }
      if (emailInput.textLength < 1) {
        emailInput.setAttribute("required", "required");
      }
      if (telInput.textLength < 1) {
        telInput.setAttribute("required", "required");
      }

      inputElement.classList.toggle("conditions-input-checked");

      if (
        inputElement.classList.contains("conditions-input-checked") &&
        nameInput.value.search(/^[А-Яа-яЁё\s-]+$/) === 0 &&
        emailInput.value.search(/^[^@\s]+@[^@\s]+\.[^@\s]+$/) === 0 &&
        telInput.value.search(
          /\+?\d{1,4}?[-.\s]?\(?\d{1,3}?\)?[-.\s]?\d{1,4}[-.\s]?\d{1,4}[-.\s]?/
        ) === 0
      ) {
        buttonElement.disabled = false;
      } else {
        buttonElement.disabled = true;
      }
    },
  },

  data() {
    return {
      languages: [
        { title: "Русский", checked: true, id: 0 },
        { title: "Английский", id: 1 },
        { title: "Китайский", id: 2 },
        { title: "Испанский", id: 3 },
      ],
    };
  },
};
</script>
