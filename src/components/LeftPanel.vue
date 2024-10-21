<template>
  <aside :class="['left-panel', { 'is-hidden': !isVisible && isMobile }]">
    <div class="left-panel__logo">
      <img src="../assets/logo.svg" alt="Logo" />
    </div>
    <div class="left-panel__text">
      <p>How much fun<br>do you want in your life?</p>
    </div>
    <div class="left-panel__content">
      <div class="left-panel__content__email">
        <span>harry.simon@yahoo.com</span>
      </div>
      <small class="darker-gray">FUN YOU GET</small>
      <div class="left-panel__content__progress">
        <div class="progress-bar">
          <div class="progress-bar__settings" :style="{
            width: progress + '%',
            backgroundColor: 'orange',
            borderTopRightRadius: progress === 100 ? '8px' : '0',
            borderBottomRightRadius: progress === 100 ? '8px' : '0'
          }">
          </div>
        </div>
        <div class="percent">{{ progress }}%</div>
      </div>
      <div class="left-panel__content__message">
        <span class="highlight">Subscribe</span> to all our fun sites to upgrade your fun progress
      </div>
    </div>
    <div class="left-panel__bottom-content">
      <div class="left-panel__bottom-content__address">
        <small>
          EntertainMeMore<br>
          11807 Westheimer 550 PMB617<br>
          Houston, TX 77077
        </small>
      </div>
      <div class="left-panel__bottom-content__email">
        <small><a href="mailto:contact@mail.com">contact@mail.com</a></small>
      </div>
      <div class="left-panel__bottom-content__privacy">
        <small><a href="#">Privacy Policy</a></small>
      </div>
    </div>
    <button class="toggle-btn" @click="togglePanel" title="Click me!">☰</button>
  </aside>
</template>

<script lang="ts">
export default {
  props: {
    progress: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      isVisible: true,
      isMobile: false
    };
  },
  mounted() {
    this.updateMobileView();
    window.addEventListener('resize', this.updateMobileView);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.updateMobileView);
  },
  methods: {
    togglePanel() {
      this.isVisible = !this.isVisible;
    },
    updateMobileView() {
      this.isMobile = window.innerWidth < 1024;
    }
  }
};
</script>

<style scoped>

</style>
