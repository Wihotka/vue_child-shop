<template>
  <footer class="footer">
    <div class="lists-block">
      <div class="block-first">
        <h6 class="block-title">покупателям</h6>
        <ul class="list">
          <li v-for="(item, index) in listFirst" :key="index" class="list-item">
            <a href="#" class="list-link">{{ item }}</a>
          </li>
        </ul>
      </div>
      <div class="block-second">
        <h6 class="block-title">о нас</h6>
        <ul class="list">
          <li v-for="(item, index) in listSecond" :key="index" class="list-item">
            <a href="#" class="list-link">{{ item }}</a>
          </li>
        </ul>
      </div>
    </div>
    <form novalidate="true" @submit="checkErrors" class="email-form">
      <h6 class="block-title email-title">Узнайте первыми о новинках и акциях</h6>
      <label class="email-block">
        <input
          type="email"
          placeholder="Адрес электронной почты"
          :error="emailErrors[0]"
          v-model.trim="email"
          @input="clearEmailError"
          @blur="checkEmail"
          class="email-input"
          :class="emailErrors[0] ? 'error' : ''"
        >
        <span :error="emailErrors[0]" class="email-error">{{ emailErrors[0] }}</span>
        <button class="email-clean" @click="clearEmail">
          <svg class="clean-icon">
            <use xlink:href="@/assets/sprite.svg#close-icon"></use>
          </svg>
        </button>
      </label>
      <button type="submit" class="subscribe-btn">Подписаться</button>
    </form>
  </footer>
</template>

<script>
  export default {
    data() {
      return {
        listFirst: ['Каталог', 'Акции', 'Бренды'],
        listSecond: ['О компании', 'Новости', 'Команда'],
        emailErrors: [],
        email: null
      }
    },
    methods: {
      clearEmailError: function(e) {
        e.preventDefault();

        this.emailErrors = [];

        return true;
      },
      checkEmail: function(e) {
        e.preventDefault();

        this.emailErrors = [];

        if (!this.email) {
          this.emailErrors.push('Укажите вашу электронную почту.');
          console.log(this.emailErrors);
        } else if (!this.validEmail(this.email)) {
          this.emailErrors.push('Укажите корректный адрес электронной почты.');
          console.log(this.emailErrors);
        }

        if (!this.emailErrors.length) {
          return true;
        }
      },
      validEmail: function(email) {
        const regExp = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        return regExp.test(email);
      },
      clearEmail: function(e) {
        e.preventDefault();

        this.emailErrors = [];
        this.email = null;

        return true;
      },
      checkErrors: function(e) {
        e.preventDefault();

        if (this.email && !this.emailErrors.length) {
          alert('Заявка отправлена');
          this.email = null;
        } else {
          this.checkEmail(e);
        }
      }
    }
  }
</script>

<style scoped>
  .footer {
    display: grid;
    grid-template-rows: repeat(2, 1fr);
    grid-template-columns: 1fr;
    margin-bottom: 186px;
    padding: 0 20px;
  }

  .lists-block {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 9px;
    margin-bottom: 58px;
  }

  .block-title {
    max-width: 255px;
    margin: 0;
    margin-bottom: 16px;
    font-weight: normal;
    font-size: 16px;
    line-height: 24px;
    text-transform: uppercase;
  }

  .list-item {
    margin-bottom: 8px;
  }
  .list-item:last-child {
    margin-bottom: 0;
  }

  .list-link {
    color: var(--black);
    text-decoration: none;
    transition: var(--timer) ease-in-out;
  }

  .email-form {
    max-width: 452px;
  }

  .email-block {
    position: relative;
    display: block;
    margin-bottom: 25px;
  }

  .email-title {
    margin-bottom: 20px;
  }

  .email-input {
    width: 100%;
    padding: 12px 16px;
    border: none;
    border-bottom: 1px solid var(--greyLight);
    transition: var(--timer) ease-in-out;
  }
  .email-input::placeholder {
    color: var(--greyDark);
    letter-spacing: 0.04em;
  }
  .email-input.error {
    color: var(--red);
    border-color: var(--red);
  }

  .email-error {
    position: absolute;
    top: 42px;
    left: 16px;
    color: var(--red);
    font-size: 12px;
    line-height: 16px;
  }

  .email-clean {
    position: absolute;
    top: 5px;
    right: 5px;
    padding: 6px;
    border: none;
    background-color: var(--white);
    cursor: pointer;
  }

  .clean-icon {
    width: 10px;
    height: 10px;
    color: var(--greyLight);
    transition: var(--timer) ease-in-out;
  }

  .subscribe-btn {
    display: block;
    margin-left: auto;
    padding: 9px 27px;
    border: 1px solid var(--black);
    background-color: var(--white);
    letter-spacing: 0.04em;
    transition: var(--timer) ease-in-out;
    cursor: pointer;
  }

  /* active & focus states */
  .list-link:focus {
    color: var(--orangeDark);
    outline: none;
  }
  .list-link:active {
    color: var(--orangeLight);
  }

  .email-input:focus {
    border-color: var(--orangeDark);
    outline: none;
  }

  .email-clean:focus {
    outline: none;
  }
  .email-clean:focus .clean-icon {
    color: var(--orangeDark);
  }
  .email-clean:active .clean-icon {
    color: var(--orangeLight);
  }

  .subscribe-btn:focus {
    border-color: var(--orangeDark);
    color: var(--orangeDark);
    outline: none;
  }
  .subscribe-btn:active {
    border-color: var(--orangeLight);
    color: var(--orangeLight);
    outline: none;
  }

  @media (hover: hover) {
    .list-link:hover {
      color: var(--orange);
    }
    .list-link:active {
      color: var(--orangeLight);
    }

    .email-input:hover {
      border-color: var(--orange);
    }
    .email-input.error:hover {
      border-color: var(--red);
    }

    .email-clean:hover .clean-icon {
      color: var(--orange);
    }
    .email-clean:active .clean-icon {
      color: var(--orangeLight);
    }

    .subscribe-btn:hover {
      border-color: var(--orange);
      color: var(--orange);
    }
    .subscribe-btn:active {
      border-color: var(--orangeLight);
      color: var(--orangeLight);
      outline: none;
    }
  }

  @media all and (min-width: 768px) {
    .footer {
      grid-template-rows: 1fr;
      grid-template-columns: repeat(2, 1fr);
      margin-bottom: 70px;
      padding: 0 40px;
    }

    .email-form {
      width: 100%;
    }

    .email-title {
      max-width: 100%;
    }
  }

  @media all and (min-width: 1390px) {
    .footer {
      padding: 0 117px;
    }

    .lists-block {
      grid-template-columns: repeat(2, minmax(min-content, auto));
      gap: 9px;
      justify-content: space-between;
      margin-bottom: 0;
      padding-right: 136px;
    }

    .email-form {
      width: 452px;
      margin-left: auto;
    }

    .email-block {
      margin-bottom: 36px;
    }

    .email-title {
      margin-bottom: 34px;
    }
  }
</style>
