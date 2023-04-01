<script setup>
defineProps({
  isNotification: {
    type: Boolean,
  },
  totalNotification: {
    type: Number,
  },
});
</script>

<template>
  <div class="nav__icon">
    <a href="#">
      <div
        v-if="isNotification"
        class="nav__icon--notification"
      >
        <p>{{ totalNotification }}</p>
      </div>
      <slot></slot>
      <!-- <i><img :src="iconUrl" alt="" /></i> -->
    </a>
  </div>
</template>

<style lang="scss">
.nav__icon {
  padding: 8px;
  position: relative;

  &--notification {
    width: fit-content;
    padding: 2px 4px;
    text-align: center;
    border-radius: 100px;
    color: white;
    background-color: #ec3131;
    border: none;
    font-size: 10px;
    position: absolute;
    right: 4px;
    top: 4px;

    p {
      font-size: 10px;
      line-height: 1;
    }
  }
}
</style>
