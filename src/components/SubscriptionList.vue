<template>
  <main class="subscription-list">
    <div class="subscription-list__info">
      <h2>Ok, let’s change your preferences.</h2>
      <button class="button-primary" @click="unsubscribeFromAll">Unsubscribe from all</button>
    </div>
    <p class="subscription-list__text">
      To unsubscribe, please uncheck the appropriate box(es).
    </p>
    <div class="subscription-list__banners">
      <div class="subscription-banners" v-for="site in sites" :key="site.site">
        <div class="subscription-banners__logo">
          <img :src="site.img" :alt="site.site" class="site-logo"/>
        </div>
        <div class="subscription-banners__text">
          <p>{{ truncateText(site.text, 64) }}</p>
        </div>
        <div class="subscription-banners__footer">
          <button
              :class="[
              'subscribe-button',
              site.subscribed ? 'subscribed-button' : 'subscribe-button-regular'
            ]"
              @click="toggleSubscribe(site)"
          >
            <span v-if="site.subscribed" class="subscribed-text">
              <img src="/src/assets/icons/check.svg" alt="Check icon"> Subscribed
            </span>
            <span v-else class="subscribe-text">Subscribe</span>
          </button>
        </div>
      </div>
    </div>
  </main>
  <Modal v-if="showModal" :oldFun="oldFun" :newFun="funPercentage" :visible="showModal" @close="closeModal"/>
</template>

<script lang="ts">
import { ref, watchEffect } from 'vue';
import subscribeData from '../Subscribe.json';
import Modal from "./Modal.vue";

export default {
  components: { Modal },
  emits: ['update-progress'],
  setup(_, context) {
    const sites = ref(subscribeData);
    const funPercentage = ref(0);
    const oldFun = ref(0);
    const showModal = ref(false);

    const updateFunProgress = () => {
      const subscribedCount = sites.value.filter(site => site.subscribed).length;
      funPercentage.value = Math.round((subscribedCount / sites.value.length) * 100);
      context.emit('update-progress', funPercentage.value);
    };

    const unsubscribeFromAll = () => {
      oldFun.value = funPercentage.value;
      sites.value.forEach(site => site.subscribed = false);
      updateFunProgress();
      showModal.value = true;

      const currentState = sites.value.map(site => ({
        site: site.site,
        subscribed: site.subscribed
      }));
      console.log("Current subscriptions state:", JSON.stringify(currentState));
    };

    const closeModal = () => {
      showModal.value = false;
    };

    const toggleSubscribe = (site) => {
      site.subscribed = !site.subscribed;
      updateFunProgress();

      const currentState = sites.value.map(site => ({
        site: site.site,
        subscribed: site.subscribed
      }));
      console.log("Current subscriptions state:", JSON.stringify(currentState));
    };

    watchEffect(() => {
      updateFunProgress();
    });

    const truncateText = (text: string, maxLength: number) => {
      return text.length > maxLength ? text.substring(0, maxLength) + '...' : text;
    };

    return {
      sites,
      funPercentage,
      oldFun,
      showModal,
      truncateText,
      unsubscribeFromAll,
      closeModal,
      toggleSubscribe
    };
  }
};
</script>
