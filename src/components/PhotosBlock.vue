<template>
  <div class="photos-block">
    <a href="#" class="styles-link">Посмотреть все стили</a>
    <div class="photos">
      <a href="#" v-for="photo in photos" :key="photo.id" class="photo-link">
        <img :src="photo.url" alt="child photo" class="photo-img">
        <div class="link-canvas">
          <svg class="multiple-icon">
            <use xlink:href="@/assets/sprite.svg#multiple-icon"></use>
          </svg>
          <div class="about-me">
            <svg class="about-me-icon">
              <use xlink:href="@/assets/sprite.svg#about-me-icon"></use>
            </svg>
            <span class="about-me-text">Узнай, что на мне</span>
          </div>
          <div class="likes">
            <svg class="likes-icon">
              <use xlink:href="@/assets/sprite.svg#favorite-icon"></use>
            </svg>
            <span class="likes-text">{{ photo.likes }}</span>
          </div>
        </div>
      </a>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        photos: [
          {
            url: require('@/assets/photos/1.jpg'),
            likes: '312',
            id: '1'
          },
          {
            url: require('@/assets/photos/2.jpg'),
            likes: '300',
            id: '2'
          },
          {
            url: require('@/assets/photos/3.jpg'),
            likes: '256',
            id: '3'
          },
          {
            url: require('@/assets/photos/4.jpg'),
            likes: '200',
            id: '4'
          },
          {
            url: require('@/assets/photos/5.jpg'),
            likes: '103',
            id: '5'
          }
        ]
      }
    },
  }
</script>

<style scoped>
  .photos-block {
    margin-bottom: 40px;
  }

  .styles-link {
    display: block;
    margin: 58px 0;
    color: var(--black);
    text-align: center;
    transition: var(--timer) ease-in-out;
  }

  .photos {
    display: grid;
    grid-template-rows: repeat(4, 1fr);
    grid-template-columns: repeat(2, 1fr);
    gap: 8px;
  }

  .photo-link {
    position: relative;
    display: block;
    transition: var(--timer) ease-in-out;
  }
  .photo-link:first-child {
    grid-row: 1 / span 2;
    grid-column: 1 / span 2;
  }

  .photo-img {
    display: block;
    width: 100%;
    height: auto;
  }

  .link-canvas {
    position: absolute;
    top: 0;
    left: 0;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    height: 100%;
    padding: 16px;
    background-color: var(--blackOpacity);
    visibility: hidden;
    opacity: 0;
    transition: var(--timer) ease-in-out;
  }

  .multiple-icon {
    width: 16px;
    height: 16px;
    margin-left: auto;
    color: var(--white);
    fill: none;
  }

  .about-me {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .about-me-icon {
    width: 32px;
    height: 34px;
    margin-bottom: 7px;
    color: var(--white);
    fill: none;
  }

  .about-me-text {
    color: var(--white);
  }

  .likes {
    display: flex;
  }

  .likes-icon {
    width: 24px;
    height: 24px;
    padding: 4px;
    margin-right: 2px;
    color: var(--white);
    fill: var(--white);
  }

  .likes-text {
    color: var(--white);
  }

  /* active & focus states */
  .styles-link:focus {
    color: var(--orangeDark);
    outline: none;
  }
  .styles-link:active {
    color: var(--orangeLight);
  }

  .photo-link:active {
    opacity: 0.75;
  }
  .photo-link:focus {
    outline: none;
  }
  .photo-link:focus .link-canvas {
    visibility: visible;
    opacity: 1;
  }

  @media (hover: hover) {
    .styles-link:hover {
      color: var(--orange);
    }
    .styles-link:active {
      color: var(--orangeLight);
    }

    .photo-link:hover .link-canvas {
      visibility: visible;
      opacity: 1;
    }
  }

  @media all and (min-width: 768px) {
    .styles-link {
      margin: 32px 0;
    }

    .photos {
      grid-template-rows: repeat(2, 1fr);
      grid-template-columns: repeat(4, 1fr);
      gap: 8px;
    }
  }

  @media all and (min-width: 1390px) {
    .photos-block {
      margin-bottom: 142px;
    }

    .photos {
      gap: 16px;
    }
  }
</style>
