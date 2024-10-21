<template>
  <left-panel :progress="progress" />
  <subscription-list @update-progress="updateProgress" />
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
