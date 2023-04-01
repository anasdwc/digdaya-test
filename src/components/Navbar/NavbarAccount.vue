<script setup>
import IconItem from "./IconItem.vue";
import IconDown from "../icons/IconDown.vue";
</script>

<template>
  <div class="nav__account">
    <div class="nav__account__name">
      <div class="rounded-img">
        <div class="rounded-img--online"></div>
      </div>
      <p>Bryan Adams</p>
    </div>
    <IconItem>
      <IconDown />
    </IconItem>
  </div>
</template>

<style lang="scss">
.nav__account {
  display: flex;
  align-items: center;
  cursor: pointer;

  p {
    font-size: 12px;
  }

  &__name {
    padding: 8px;
    padding-right: 0;
    gap: 8px;
    display: flex;
    align-items: center;
  }

  .rounded-img {
    width: 32px;
    height: 32px;
    border-radius: 50%;
    background-color: white;
    position: relative;

    &--online {
      height: 10px;
      background-color: #29ccb0;
      width: 10px;
      border-radius: 50%;
      border: 2px solid #643dff;

      position: absolute;
      bottom: 0;
      right: 0;
    }
  }
}
</style>
