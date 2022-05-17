<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div class="modal">
        <header class="modal-header">
          <slot name="header">
            <button
              type="button"
              class="btn-close"
              @click="close"
            >
              <svg class="close-svg">
                <use xlink:href="@/assets/sprite.svg#close-icon"></use>
              </svg>
            </button>
          </slot>
        </header>
        <section class="modal-body">
          <slot name="body">
            {{ text }}
          </slot>
        </section>
      </div>
    </div>
  </transition>
</template>

<script>
  export default {
    name: 'modal-block',
    created() {
      window.addEventListener('click', this.clickOut);
    },
    destroyed () {
      window.removeEventListener('click', this.clickOut);
    },
    props : {
      text: String
    },
    methods: {
      close() {
        this.$emit('close');
      },
      clickOut(e) {
        if (e.target === this.$el) {
          this.$emit('close');
        }
      }
    },
  };
</script>

<style scoped>
  .modal-fade-enter,
  .modal-fade-leave-active {
    opacity: 0;
  }

  .modal-fade-enter-active,
  .modal-fade-leave-active {
    transition: opacity .45s ease;
  }

  .modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 2;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: var(--blackOpacity);
  }

  .modal {
    display: flex;
    flex-direction: column;
    min-width: 375px;
    max-width: 375px;
    border: none;
    border-radius: 2px;
    background: var(--white);
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
  }

  .modal-header {
    display: flex;
  }

  .modal-header {
    justify-content: space-between;
  }

  .modal-body {
    position: relative;
    padding: 0 54px 20px;
    color: var(--black);
    font-size: 16px;
    line-height: 22px;
    text-align: center;
  }

  .btn-close {
    display: block;
    margin-left: auto;
    padding: 12px;
    border: none;
    color: var(--greyDark);
    background: transparent;
    cursor: pointer;
  }

  .close-svg {
    width: 16px;
    height: 16px;
  }
</style>
