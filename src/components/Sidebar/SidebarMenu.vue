<template>
  <div class="sidebar__menu">
    <div class="sidebar__menu__list">
      <slot></slot>
    </div>
  </div>
</template>

<style lang="scss">
.sidebar__menu {
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  &__list {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }
}
</style>
