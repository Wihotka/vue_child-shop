<template>
  <div id="app">
    <h1 class="visually-hidden">Alef Development Testwork</h1>
    <HeaderBlock />
    <main>
      <MainBlock />
      <PhotosBlock />
    </main>
    <FooterBlock />
  </div>
</template>

<script>
  import HeaderBlock from '@/components/HeaderBlock.vue';
  import MainBlock from '@/components/MainBlock.vue';
  import PhotosBlock from '@/components/PhotosBlock.vue';
  import FooterBlock from '@/components/FooterBlock.vue';

  export default {
    name: 'App',
    data() {
      return {
        todos: ['Ремонт', 'Завтрак']
      }
    },
    components: {
      HeaderBlock,
      MainBlock,
      PhotosBlock,
      FooterBlock,
    },
    methods: {

    }
  }
</script>

<style>
  @import '~normalize.css';

  :root {
    /* colors */
    --black: #333;
    --blackOpacity: rgba(51, 51, 51, 0.7);
    --white: #fff;
    --greyDark: #828282;
    --grey: #f2f2f2;
    --greyLight: #c4c4c4;
    --orangeDark: #a74b00;
    --orange: #ff7300;
    --orangeLight: #ffac67;
    --red: #ec2d2d;
    /* animation */
    --timer: 150ms;
  }

  @font-face {
    font-family: 'Open Sans';
      src:
      local('Open Sans'),
      url('@/assets/fonts/open-sans-v18-latin_cyrillic-regular.woff2') format('woff2'),
      url('@/assets/fonts/open-sans-v18-latin_cyrillic-regular.woff') format('woff');
    font-display: swap;
    font-weight: normal;
    font-style: normal;
  }

  @font-face {
    font-family: 'Open Sans';
      src:
      local('Open Sans'),
      url('@/assets/fonts/open-sans-v18-latin_cyrillic-600.woff2') format('woff2'),
      url('@/assets/fonts/open-sans-v18-latin_cyrillic-600.woff') format('woff');
    font-display: swap;
    font-weight: 600;
    font-style: normal;
  }

  @font-face {
    font-family: 'Open Sans';
      src:
      local('Open Sans'),
      url('@/assets/fonts/open-sans-v18-latin_cyrillic-700.woff2') format('woff2'),
      url('@/assets/fonts/open-sans-v18-latin_cyrillic-700.woff') format('woff');
    font-display: swap;
    font-weight: 700;
    font-style: normal;
  }

  * {
    box-sizing: border-box;
  }

  ul {
    margin: 0;
    padding: 0;
  }

  li {
    list-style: none;
  }

  .visually-hidden {
    position: absolute;
    clip: rect(1px 1px 1px 1px); /* IE6, IE7 */
    clip: rect(1px, 1px, 1px, 1px);
    padding: 0;
    border: 0;
    height: 1px;
    width: 1px;
    overflow: hidden;
  }

  #app {
    position: relative;
    min-width: 375px;
    max-width: 100%;
    margin: 0 auto;
    padding: 68px 0 0;
    color: var(--black);
    background-color: var(--white);
    font-family: 'Open Sans', Arial, sans-serif;
    font-style: normal;
    font-weight: normal;
    font-size: 14px;
    line-height: 20px;
    letter-spacing: 0.04em;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  @media all and (min-width: 1390px) {
    #app {
      max-width: 1390px;
      padding: 64px 20px 0;
    }
  }

  @media all and (min-width: 1430px) {
    #app {
      padding: 64px 0 0;
    }
  }
</style>
