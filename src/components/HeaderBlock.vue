<template>
  <header class="header-container" :class="{hide: !isVisible}">
    <div class="header">
      <h2 class="logo">LOGO</h2>
      <div class="actions">
        <button class="actions__btn">
          <svg class="actions__svg">
            <use xlink:href="@/assets/sprite.svg#user-icon"></use>
          </svg>
        </button>
        <button class="actions__btn">
          <svg class="actions__svg">
            <use xlink:href="@/assets/sprite.svg#favorite-icon"></use>
          </svg>
        </button>
        <button class="actions__btn">
          <svg class="actions__svg">
            <use xlink:href="@/assets/sprite.svg#cart-icon"></use>
          </svg>
        </button>
      </div>
      <button @click="toggleNav" class="burger">
        <svg class="burger__svg">
          <use xlink:href="@/assets/sprite.svg#burger-icon"></use>
        </svg>
      </button>
      <div class="nav-menu" :class="{open: isNavOpen}">
        <button @click="toggleNav" class="close-btn">
          <svg class="close-btn__svg">
            <use xlink:href="@/assets/sprite.svg#close-icon"></use>
          </svg>
        </button>
        <ul>
          <li class="nav-item">
            <a href="#" class="nav-link">постельное белье</a>
          </li>
          <li class="nav-item">
            <a href="#" class="nav-link">одежда для дома</a>
          </li>
          <li class="nav-item">
            <a href="#" class="nav-link">одежда для улицы</a>
          </li>
          <li class="nav-item">
            <a href="#" class="nav-link">выход</a>
          </li>
        </ul>
      </div>
    </div>
  </header>
</template>

<script>
  export default {
    data() {
      return {
        isVisible: true,
        isNavOpen: false
      }
    },
    created() {
      window.addEventListener('mousewheel', this.mouseWheel);
      window.addEventListener('click', this.closeNav);
    },
    destroyed () {
      window.removeEventListener('mousewheel', this.mouseWheel);
      window.removeEventListener('click', this.closeNav);
    },
    methods: {
      mouseWheel: function(e) {
        if (!this.isNavOpen) {
          if (e.wheelDelta < 0) {
            this.isVisible = false;
          } else {
            this.isVisible = true;
          }
        }
      },
      toggleNav: function() {
        this.isNavOpen = !this.isNavOpen;
      },
      closeNav: function(e) {
        if (this.isNavOpen) {
          if (!this.$el.contains(e.target)) {
            this.isNavOpen = false;
          }
        }
      }
    }
  }
</script>

<style scoped>
  .header-container {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1;
    width: 100%;
    transition: var(--timer) ease-in-out;
  }
  .hide.header-container {
    visibility: hidden;
    opacity: 0;
  }

  .header {
    position: relative;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    min-width: 375px;
    max-width: 100%;
    height: 68px;
    margin: 0 auto;
    padding: 0 20px;
    background-color: var(--white);
  }

  .logo {
    margin-right: auto;
    padding-bottom: 8px;
    font-weight: 700;
    font-size: 22px;
    line-height: 16px;
  }

  .actions {
    display: flex;
    margin-right: 26px;
    padding-bottom: 4px;
  }

  .actions__btn {
    margin-right: 28px;
    padding: 4px 2px;
    border: none;
    background-color: var(--white);
    cursor: pointer;
  }

  .actions__btn:last-child {
    margin-right: 0;
  }

  .actions__svg {
    width: 16px;
    height: 16px;
    color: var(--black);
    fill: none;
    transition: var(--timer) ease-in-out;
  }

  .burger {
    display: block;
    padding: 4px 3px 9px;
    border: none;
    background-color: var(--white);
    cursor: pointer;
  }

  .burger__svg {
    width: 18px;
    height: 13px;
    color: var(--black);
    fill: none;
    transition: var(--timer) ease-in-out;
  }

  .nav-menu {
    position: absolute;
    top: 0;
    left: 0;
    display: block;
    width: 100%;
    padding: 80px 30px 43px;
    background-color: var(--white);
    font-size: 12px;
    line-height: 16px;
    text-transform: uppercase;
    visibility: hidden;
    transform-origin: top;
    transform: scaleY(0);
    transition: .3s ease-in-out;
  }
  .open.nav-menu {
    visibility: visible;
    transform: scaleY(1);
  }

  .nav-item {
    margin-bottom: 30px;
  }
  .nav-item:last-child {
    margin-bottom: 0;
  }

  .nav-link {
    color: var(--black);
    text-decoration: none;
  }

  .close-btn {
    position: absolute;
    top: 23px;
    right: 25px;
    display: block;
    padding: 5px;
    border: none;
    background-color: transparent;
    cursor: pointer;
  }

  .close-btn__svg {
    width: 14px;
    height: 14px;
    color: var(--black);
    transition: var(--timer) ease-in-out;
  }

  /* active & focus states */
  .burger:focus {
    outline: none;
  }
  .burger:focus .burger__svg {
    color: var(--orangeDark);
  }
  .burger:active .burger__svg {
    color: var(--orangeLight);
  }

  .actions__btn:focus {
    outline: none;
  }
  .actions__btn:focus .actions__svg {
    color: var(--orangeDark);
  }
  .actions__btn:active .actions__svg {
    color: var(--orangeLight);
  }

  .close-btn:focus {
    outline: none;
  }
  .close-btn:focus .close-btn__svg {
    color: var(--orangeDark);
  }
  .close-btn:active .close-btn__svg {
    color: var(--orangeLight);
  }

  .nav-link:focus {
    color: var(--orangeDark);
    outline: none;
  }
  .nav-link:active {
    color: var(--orangeLight);
  }

  @media (hover: hover) {
    .burger:hover .burger__svg,
    .actions__btn:hover .actions__svg {
      color: var(--orange);
    }
    .burger:active .burger__svg,
    .actions__btn:active .actions__svg {
      color: var(--orangeLight);
    }

    .close-btn:hover .close-btn__svg {
      color: var(--orange);
    }
    .close-btn:active .close-btn__svg {
      color: var(--orangeLight);
    }

    .nav-link:hover {
      color: var(--orange);
    }
    .nav-link:active {
      color: var(--orangeLight);
    }
  }

  @media all and (min-width: 768px) {
    .actions {
      margin-right: 0;
    }

    .burger {
      display: none;
    }

    .nav-menu {
      display: none;
    }
  }

  @media all and (min-width: 1390px) {
    .header-container {
      box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    }

    .header {
      max-width: 1390px;
      height: 40px;
      padding: 0 20px;
    }

    .logo {
      padding: 0;
    }

    .actions {
      padding-right: 5px;
      padding-bottom: 0;
    }
  }

  @media all and (min-width: 1430px) {
    .header {
      padding: 0;
    }
  }
</style>
