<template>
  <div class="main-container">
    <MainPhoto />
    <MainForm />
  </div>
</template>

<script>
  import MainPhoto from '@/components/MainPhoto.vue';
  import MainForm from '@/components/MainForm.vue';

  export default {
    components: {
      MainPhoto,
      MainForm
    }
  }
</script>

<style scoped>
  .main-container {
    display: grid;
    grid-template-columns: 1fr;
    gap: 0;
    width: 100%;
    height: fit-content;
  }

  @media all and (min-width: 768px) {
    .main-container {
      grid-template-columns: 1fr 1fr;
      gap: 8px;
      width: 100%;
      height: fit-content;
    }
  }

  @media all and (min-width: 1390px) {
    .main-container {
      gap: 16px;
    }
  }
</style>
