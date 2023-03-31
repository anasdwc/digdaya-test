<script setup>
defineProps({
  title: {
    type: String,
    required: true,
  },
  isActive: {
    type: Boolean,
  },
});
</script>

<template>
  <div
    class="sidebar__menu__item"
    :class="{ 'sidebar__menu__item--active': isActive }"
  >
    <slot></slot>
    <p>{{ title }}</p>
  </div>
</template>

<style lang="scss">
.sidebar__menu__item {
  padding: 12px;
  display: flex;
  align-items: center;
  gap: 8px;

  &--active {
    background-color: #f0ecff;
    border-radius: 8px;

    & p {
      font-weight: 700;
      color: #643dff;
    }
  }
}
</style>
