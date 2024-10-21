<template>
  <aside class="left-panel">
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
      <div class="left-panel__content__progress">
        <div class="progress-bar" :style="{ width: progress + '%', backgroundColor: 'orange', borderTopRightRadius: progress === 100 ? '8px' : '0',
            borderBottomRightRadius: progress === 100 ? '8px' : '0' }"></div>
        <small>{{ progress }}% FUN YOU GET</small>
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
  </aside>
</template>

<script lang="ts">
export default {
  props: {
    progress: {
      type: Number,
      required: true
    }
  }
};
</script>

<style scoped>

</style>
