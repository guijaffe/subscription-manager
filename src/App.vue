<template>
  <div class="container">
    <left-panel :progress="progress" />
    <div class="main-content">
      <subscription-list @update-progress="updateProgress" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import LeftPanel from './components/LeftPanel.vue';
import SubscriptionList from './components/SubscriptionList.vue';

const progress = ref(0);

const updateProgress = (newProgress: number) => {
  progress.value = newProgress;
};
</script>

<style scoped>

</style>
