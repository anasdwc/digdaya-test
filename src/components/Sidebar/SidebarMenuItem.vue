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
  cursor: pointer;
  padding: 12px;
  display: flex;
  align-items: center;
  gap: 8px;
  border-radius: 8px;

  &:hover {
    background-color: #f0ecff;
  }

  &--active {
    background-color: #f0ecff;

    & p {
      font-weight: 700;
      color: #643dff;
    }
  }
}
</style>
