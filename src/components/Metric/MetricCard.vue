<script setup>
defineProps({
  title: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <div class="metric__item">
    <div class="metric__item__header">
      <slot></slot>
      <p>Total Data</p>
    </div>
    <div class="metric__item__body">
      <p>{{ title }}</p>
    </div>
  </div>
</template>

<style lang="scss">
.metric__item {
  background-color: #fff;
  padding: 24px;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  gap: 16px;
  flex: 1;
  box-shadow: 0px 4px 30px rgba(26, 28, 33, 0.08);

  &__header {
    display: flex;
    align-items: center;
    gap: 8px;

    p {
      color: #858d9d;
      font-weight: 500;
    }
  }

  &__body p {
    color: #333843;
    font-weight: 600;
    font-size: 20px;
  }
}
</style>
