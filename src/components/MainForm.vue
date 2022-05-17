<template>
  <div>
    <ModalBlock
      v-show="isModalVisible"
      @close="closeModal"
      :text="'Товар ' + item + ', размер: ' + dropdown + ' в количестве ' + counter + ' единиц добавлен в ' + category"
    />
    <div class="main-block">
      <h4 class="heading">{{ item }}</h4>
      <span class="label">Арт. 02765/46</span>
      <a href="#" class="response-link">
        <span class="response__name">Отзывы</span>
        <div class="rating">
          <svg v-for="(star, index) in stars" :key="index" class="rating__star" :class="star ? 'rating__star-full' : 'rating__star-empty'">
            <use xlink:href="@/assets/sprite.svg#star-full-icon"></use>
          </svg>
        </div>
        <span class="response__count">14 отзывов</span>
        <div class="arrow"></div>
      </a>
      <div>
        <a href="#" class="price-link">
          <h3 class="price__current">800 ₽</h3>
          <span class="price__old">1 500 ₽</span>
          <div class="arrow"></div>
        </a>
        <div class="discounts">
          <div class="discount">скидка -36%</div>
          <div class="discount">акция -20%</div>
        </div>
        <div class="dropdown-container">
          <div tabindex="0" @click="toggleDropdown" class="dropdown" :class="{error: isDropdownError}">
            <span>{{ dropdown }}</span>
            <div class="arrow-down" :class="{open: isDropdownOpen}"></div>
          </div>
          <ul class="dropdown-list" :class="{open: isDropdownOpen}">
            <li v-for="(size, index) in sizes" :key="index" @click="chooseDropdown" class="dropdown-item">{{ size }}</li>
          </ul>
        </div>
        <a href="#" class="link learn-size">Определить размер</a>
        <div class="add-block">
          <div class="counter">
            <button class="counter__btn" @click="addCounter">+</button>
            <span class="counter__num">{{ counter }}</span>
            <button class="counter__btn" @click="subtractCounter">-</button>
          </div>
          <div class="btns">
            <button @click="showModal" class="add-btn" :id="isCart">Добавить в корзину</button>
            <button @click="showModal" class="favorite-btn">
              <svg class="favorite__svg">
                <use xlink:href="@/assets/sprite.svg#favorite-icon"></use>
              </svg>
            </button>
          </div>
        </div>
        <a href="#" class="link quick-buy">Купить в 1 клик</a>
      </div>
    </div>
    <hr class="horizon-line">
    <div class="additional-links">
      <a href="#" class="link additional-link">
        <svg class="additional-icon">
          <use xlink:href="@/assets/sprite.svg#clothes-icon"></use>
        </svg>
        <span>Описание товара</span>
      </a>
      <a href="#" class="link additional-link">
        <svg class="additional-icon">
          <use xlink:href="@/assets/sprite.svg#time-icon"></use>
        </svg>
        <span>Доставка и возврат</span>
      </a>
      <a href="#" class="link additional-link">
        <svg class="additional-icon">
          <use xlink:href="@/assets/sprite.svg#payment-icon"></use>
        </svg>
        <span>Способы оплаты</span>
      </a>
    </div>
  </div>
</template>

<script>
  import ModalBlock from '@/components/ModalBlock.vue';

  export default {
    data() {
      return {
        item: 'Пижама для девочек',
        category: '',
        isCart: true,
        stars: [true, true, true, true, false],
        dropdown: 'Выбрать размер',
        sizes: [
          'XXS(28) - 4 года (рост 96-104см)',
          'XS(30) - 6 лет (рост 106-116см)',
          'S(32) - 8 лет (рост 118-128см)',
          'M(34-36) - 9 лет (рост 130-140см)',
          'L(38) - 12 лет (рост 142-152см)',
        ],
        isDropdownChosen: false,
        isDropdownOpen: false,
        counter: 1,
        isModalVisible: false,
        isDropdownError: false,
      }
    },
    created() {
      window.addEventListener('click', this.closeDropdown);
    },
    destroyed () {
      window.removeEventListener('click', this.closeDropdown);
    },
    components: {
      ModalBlock
    },
    methods: {
      toggleDropdown: function() {
        this.isDropdownOpen = !this.isDropdownOpen;
      },
      chooseDropdown: function(e) {
        if (!this.isDropdownChosen) this.isDropdownChosen = true;
        if (this.isDropdownError) this.isDropdownError = false;
        this.dropdown = e.target.textContent;
        this.isDropdownOpen = !this.isDropdownOpen;
      },
      closeDropdown: function(e) {
        if (this.isDropdownOpen) {
          const dropdownContainer = this.$el.children[1].children[3].children[2];
          if (!dropdownContainer.contains(e.target)) {
            this.isDropdownOpen = false;
          }
        }
      },
      addCounter: function() {
        if (this.counter < 99) {
          this.counter++
        }
      },
      subtractCounter: function() {
        if (this.counter > 1) {
          this.counter--
        }
      },
      showModal(e) {
        if (this.isDropdownChosen) {
          this.isModalVisible = true;
          if (e.target.id) {
            this.category = 'корзину';
          } else {
            this.category = 'избранное';
          }
        } else  {
          const dropdown = this.$el.children[1].children[3].children[2].children[0];
          dropdown.focus();
          this.isDropdownError = true;
        }
      },
      closeModal() {
        this.isModalVisible = false;
      }
    }
  }
</script>

<style scoped>
  .main-block {
    width: 375px;
    padding: 24px 20px 29px;
    margin: 0 auto;
  }

  .heading {
    margin-top: 0;
    margin-bottom: 8px;
    font-weight: 600;
    font-size: 18px;
    line-height: 24px;
    letter-spacing: 0;
  }

  .label {
    display: block;
    margin-bottom: 18px;
    color: var(--greyDark);
    font-size: 12px;
    line-height: 16px;
  }

  .response-link {
    display: flex;
    align-items: center;
    margin-right: 44px;
    margin-bottom: 46px;
    color: var(--black);
    text-decoration: none;
    transition: var(--timer) ease-in-out;
  }

  .response__name {
    margin-right: 12px;
  }

  .rating {
    display: inline-block;
    margin-right: 5px;
  }

  .rating__star {
    width: 10px;
    height: 10px;
    margin-right: 2px;
    fill: none;
    transition: var(--timer) ease-in-out;
  }
  .rating__star-full {
    color: var(--black);
  }
  .rating__star-empty {
    color: var(--white);
  }
  .rating__star:last-child {
    margin-right: 0;
  }

  .response__count {
    margin-right: 4px;
  }

  .arrow {
    display: inline-block;
    width: 10px;
    height: 10px;
    border: 1px solid var(--black);
    border-left: none;
    border-bottom: none;
    transform: rotate(45deg);
    transition: var(--timer) ease-in-out;
  }

  .price-link {
    display: flex;
    align-items: center;
    margin-bottom: 12px;
    color: var(--black);
    text-decoration: none;
    transition: var(--timer) ease-in-out;
  }

  .price__current {
    margin: 0 12px 0 0;
    font-weight: 700;
    font-size: 24px;
    line-height: 24px;
    letter-spacing: 0.05em;
  }

  .price__old {
    margin-right: 15px;
    color: var(--greyDark);
    text-decoration: line-through;
    transition: var(--timer) ease-in-out;
  }

  .discounts {
    display: flex;
    margin-bottom: 32px;
  }

  .discount {
    padding: 3px 6px;
    border: 1px solid var(--black);
    font-size: 12px;
    line-height: 16px;
    margin-right: 10px;
  }

  .discount:last-child {
    margin-right: 0;
  }

  .dropdown-container {
    position: relative;
    width: 315px;
    margin-bottom: 12px;
  }

  .dropdown {
    display: flex;
    align-items: center;
    width: 100%;
    padding: 12px 15px 10px;
    border: 1px solid var(--black);
    transition: var(--timer) ease-in-out;
    cursor: pointer;
  }
  .error.dropdown {
    color: var(--red);
    border-color: var(--red);
  }
  .error.dropdown .arrow-down {
    border-color: var(--red);
  }

  .arrow-down {
    display: inline-block;
    width: 10px;
    height: 10px;
    margin-bottom: 7px;
    margin-left: auto;
    border: 1px solid var(--black);
    border-left: none;
    border-bottom: none;
    transform: rotateZ(135deg);
    transition: transform var(--timer) ease-in-out;
  }
  .open.arrow-down {
    margin-bottom: 0;
    transform: rotateZ(-45deg);
  }

  .dropdown-list {
    position: absolute;
    z-index: 1;
    width: 100%;
    border: 1px solid var(--black);
    border-top: none;
    background-color: var(--white);
    transform-origin: top;
    transform: scaleY(0);
    transition: var(--timer) ease-in-out;
    visibility: hidden;
  }
  .open.dropdown-list {
    transform: scaleY(1);
    visibility: visible;
  }

  .dropdown-item {
    width: 100%;
    padding: 7px 15px;
    transition: var(--timer) ease-in-out;
    cursor: pointer;
  }

  .link {
    display: block;
    color: var(--black);
    transition: var(--timer) ease-in-out;
  }
  .learn-size {
    margin-bottom: 40px;
  }

  .add-block {
    display: grid;
    grid-template-rows: repeat(2, minmax(min-content, auto));
    grid-template-columns: minmax(min-content, auto);
    width: fit-content;
  }

  .counter {
    display: flex;
    align-items: center;
    width: fit-content;
    margin-bottom: 15px;
    background-color: var(--grey);
  }

  .counter__btn {
    width: 44px;
    height: 44px;
    padding: 0;
    border: none;
    background-color: transparent;
    cursor: pointer;
    transition: var(--timer) ease-in-out;
  }

  .counter__num {
    padding: 12px 24px;
  }

  .btns {
    display: flex;
    width: 100%;
    height: 44px;
    margin-bottom: 21px;
  }

  .add-btn {
    margin-right: 4px;
    padding: 12px 28px;
    border: none;
    color: var(--white);
    background-color: var(--black);
    letter-spacing: 0.04em;
    transition: var(--timer) ease-in-out;
    cursor: pointer;
  }

  .favorite-btn {
    height: 100%;
    padding: 14px 14px;
    border: none;
    background-color: var(--black);
    transition: var(--timer) ease-in-out;
    cursor: pointer;
  }

  .favorite__svg {
    width: 16px;
    height: 16px;
    color: var(--white);
    fill: none;
  }

  .horizon-line {
    margin: 0;
    color: var(--greyLight);
  }

  .additional-links {
    display: flex;
    flex-direction: column;
    width: 375px;
    padding: 22px 20px 0;
    margin: 0 auto;
  }

  .additional-link {
    display: flex;
    align-items: center;
    margin-bottom: 12px;
  }
  .additional-link:last-child {
    margin-bottom: 0;
  }

  .additional-icon {
    width: 16px;
    height: 16px;
    margin-right: 6px;
    color: var(--black);
    fill: none;
    transition: var(--timer) ease-in-out;
  }

  /* active & focus states */
  .response-link:focus {
    color: var(--orangeDark);
    outline: none;
  }
  .response-link:focus .arrow {
    border-color: var(--orangeDark);
  }
  .response-link:focus .rating__star-full {
    color: var(--orangeDark);
  }
  .response-link:active {
    color: var(--orangeLight);
  }
  .response-link:active .arrow {
    border-color: var(--orangeLight);
  }
  .response-link:active .rating__star-full {
    color: var(--orangeLight);
  }

  .price-link:focus {
    color: var(--orangeDark);
    outline: none;
  }
  .price-link:focus .price__old {
    color: var(--orangeDark);
  }
  .price-link:focus .arrow {
    border-color: var(--orangeDark);
  }
  .price-link:active {
    color: var(--orangeLight);
  }
  .price-link:active .price__old {
    color: var(--orangeLight);
  }
  .price-link:active .arrow {
    border-color: var(--orangeLight);
  }

  .dropdown:focus {
    color: var(--orangeDark);
    border-color: var(--orangeDark);
    outline: none;
  }
  .dropdown:focus .arrow-down {
    border-color: var(--orangeDark);
  }
  .error.dropdown:focus {
    color: var(--red);
    border-color: var(--red);
  }
  .error.dropdown:focus .arrow-down {
    border-color: var(--red);
  }
  .dropdown:active {
    color: var(--orangeLight);
    border-color: var(--orangeLight);
  }
  .dropdown:active .arrow-down {
    border-color: var(--orangeLight);
  }

  .dropdown-item:focus {
    color: var(--orangeDark);
    background-color: var(--grey);
    outline: none;
  }
  .dropdown-item:active {
    color: var(--orangeLight);
    background-color: var(--greyLight);
  }

  .link:focus {
    color: var(--orangeDark);
    outline: none;
  }
  .link:active {
    color: var(--orangeLight);
  }

  .additional-link:focus .additional-icon {
    color: var(--orangeDark);
  }
  .additional-link:active .additional-icon {
    color: var(--orangeLight);
  }

  .counter__btn:focus {
    color: var(--orangeDark);
    background-color: var(--greyDark);
    outline: none;
  }
  .counter__btn:active {
    color: var(--orangeLight);
    background-color: var(--grey);
  }

  .add-btn:focus,
  .favorite-btn:focus {
    background-color: var(--orangeDark);
    outline: none;
  }
  .add-btn:active,
  .favorite-btn:active {
    background-color: var(--orangeLight);
  }

  @media (hover: hover) {
    .response-link:hover {
      color: var(--orange);
    }
    .response-link:hover .arrow {
      border-color: var(--orange);
    }
    .response-link:hover .rating__star-full {
      color: var(--orange);
    }
    .response-link:active {
      color: var(--orangeLight);
    }
    .response-link:active .arrow {
      border-color: var(--orangeLight);
    }
    .response-link:active .rating__star-full {
      color: var(--orangeLight);
    }

    .price-link:hover {
      color: var(--orange);
    }
    .price-link:hover .price__old {
      color: var(--orange);
    }
    .price-link:hover .arrow {
      border-color: var(--orange);
    }
    .price-link:active {
      color: var(--orangeLight);
    }
    .price-link:active .price__old {
      color: var(--orangeLight);
    }
    .price-link:active .arrow {
      border-color: var(--orangeLight);
    }

    .dropdown:hover {
      color: var(--orange);
      border-color: var(--orange);
    }
    .dropdown:hover .arrow-down {
      border-color: var(--orange);
    }
    .dropdown:active {
      color: var(--orangeLight);
      border-color: var(--orangeLight);
    }
    .dropdown:active .arrow-down {
      border-color: var(--orangeLight);
    }

    .dropdown-item:hover {
      color: var(--orange);
      background-color: var(--grey);
    }
    .dropdown-item:active {
      color: var(--orangeLight);
      background-color: var(--greyLight);
    }

    .link:hover {
      color: var(--orange);
    }
    .link:active {
      color: var(--orangeLight);
    }

    .additional-link:hover .additional-icon {
      color: var(--orange);
    }
    .additional-link:active .additional-icon {
      color: var(--orangeLight);
    }

    .counter__btn:hover {
      color: var(--orange);
      background-color: var(--greyLight);
    }
    .counter__btn:active {
      color: var(--orangeLight);
      background-color: var(--grey);
    }

    .add-btn:hover,
    .favorite-btn:hover {
      background-color: var(--orange);
    }
    .add-btn:active,
    .favorite-btn:active {
      background-color: var(--orangeLight);
    }
  }

  @media all and (min-width: 768px) {
    .main-block {
      width: 100%;
    }

    .additional-links {
      width: 100%;
    }
  }

  @media all and (min-width: 1390px) {
    .add-block {
      grid-template-rows: minmax(min-content, auto);
      grid-template-columns: repeat(2, minmax(min-content, auto));
      margin-bottom: 12px;
    }

    .counter {
      margin-right: 12px;
      margin-bottom: 0;
    }

    .btns {
      margin-bottom: 0;
    }
  }
</style>
