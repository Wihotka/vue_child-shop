<template>
  <div class="container">
    <img :src="source" alt="child photo" class="main-image" :class="{changed: isChanged}">
    <div class="more-images">
      <button
        v-for="photo in photos"
        :key="photo.id"
        :id="photo.id"
        @click="changePhoto"
        class="more-btn"
        :class="{active: photo.isActive}"
      ></button>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        photos: [
          { id: '1', src: require('@/assets/main/2.jpg'), isActive: true },
          { id: '2', src: require('@/assets/main/1.jpg'), isActive: false },
          { id: '3', src: require('@/assets/main/3.jpg'), isActive: false },
          { id: '4', src: require('@/assets/main/4.jpg'), isActive: false },
          { id: '5', src: require('@/assets/main/5.jpg'), isActive: false }
        ],
        source: require('@/assets/main/2.jpg'),
        isChanged: false,
        showModal: false
      }
    },
    methods: {
      changePhoto: function(e) {
        this.photos.forEach(photo => {
          if (photo.id === e.target.id) {
            if (!photo.isActive) {
              photo.isActive = true;
              this.isChanged = true;
              setTimeout(() => {
                this.source = photo.src;
                this.isChanged = false;
              }, 150);
            }
          } else {
            photo.isActive = false;
          }
        });
      }
    }
  }
</script>

<style scoped>
  .container {
    position: relative;
    width: fit-content;
    height: 480px;
    margin: 0 auto;
  }

  .main-image {
    display: block;
    width: 375px;
    height: 100%;
    opacity: 1;
    transition: var(--timer) ease-in-out;
  }
  .changed.main-image {
    opacity: 0;
  }

  .more-images {
    position: absolute;
    top: 28px;
    left: 24px;
    display: flex;
    flex-direction: column;
    width: fit-content;
  }

  .more-btn {
    position: relative;
    width: 40px;
    height: 52px;
    margin-bottom: 4px;
    padding: 0;
    border: 0;
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    cursor: pointer;
  }
  .more-btn::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: var(--white);
    opacity: 0.3;
    transition: var(--timer) ease-in-out;
  }
  .active.more-btn::after {
    opacity: 0;
  }

  .more-btn:nth-child(1) {
    background-image: url('@/assets/main/2.jpg');
  }
  .more-btn:nth-child(2) {
    background-image: url('@/assets/main/1.jpg');
  }
  .more-btn:nth-child(3) {
    background-image: url('@/assets/main/3.jpg');
  }
  .more-btn:nth-child(4) {
    background-image: url('@/assets/main/4.jpg');
  }
  .more-btn:nth-child(5) {
    background-image: url('@/assets/main/5.jpg');
  }

  .more-btn:last-child {
    margin-bottom: 0;
  }

  /* active & focus states */
  .more-btn:active::after {
    opacity: 0.5;
  }

  @media (hover: hover) {
    .more-btn:hover::after {
      opacity: 0;
    }
    .more-btn:active::after {
      opacity: 0.5;
    }
  }

  @media all and (min-width: 768px) {
    .main-image {
      width: 100%;
    }
  }

  @media all and (min-width: 1390px) {
    .container {
      height: 880px;
    }

    .more-images {
      top: 24px;
    }

    .more-btn {
      width: 70px;
      height: 91px;
      margin-bottom: 7px;
    }
  }
</style>
