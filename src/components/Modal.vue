<template>
  <div class="modal" v-if="visible" @mousedown="handleBackdropClick">
    <div class="modal__content">
      <header class="modal__header">
        <h2>Are you sure?</h2>
        <button class="modal__close" @click="closePopup">
          <img src="/src/assets/icons/x-icon.svg" alt="Close"/>
        </button>
      </header>
      <div class="modal__body">
        <p>Please confirm that you want to unsubscribe from all and lose {{ oldFun - newFun }}% fun.</p>
      </div>
      <footer class="modal__footer">
        <button class="button-secondary" @click="closePopup">Affirmative</button>
      </footer>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    oldFun: { type: Number, required: true },
    newFun: { type: Number, required: true },
    visible: { type: Boolean, required: true }
  },
  emits: ['close'],
  methods: {
    closePopup() {
      this.$emit('close');
    },
    handleBackdropClick(event: MouseEvent) {
      const target = event.target as HTMLElement;
      if (target === event.currentTarget) {
        this.closePopup();
      }
    }
  }
});
</script>

<style lang="scss">
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: #0C1C604D;
  backdrop-filter: blur(3px);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1050;

  &__content {
    background-color: #fff;
    padding: 20px;
    border-radius: 10px;
    width: 512px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    animation: fadeIn 0.3s ease-in-out;
  }

  &__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;

    h2 {
      margin: 0;
      font-size: 1.25rem;
    }

    &__close {
      background-color: inherit;
      border: none;
      font-size: 1.5rem;
      cursor: pointer;
    }
  }

  &__body {
    margin-bottom: 20px;
    font-size: 1rem;
    color: #555;
  }

  &__footer {
    text-align: right;

    &__confirm {
      background-color: #007BFF;
      color: #fff;
      padding: 10px 15px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: scale(0.9);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}
</style>
