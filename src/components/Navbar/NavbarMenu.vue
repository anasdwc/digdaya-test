<script setup>
import IconItem from "../IconItem.vue";
import IconEnvelope from "../icons/IconEnvelope.vue";
import IconNotification from "../icons/IconNotification.vue";
</script>

<template>
  <div class="nav__menu">
    <IconItem>
      <IconEnvelope />
    </IconItem>
    <IconItem :isNotification="true" :totalNotification="12">
      <IconNotification />
    </IconItem>
  </div>
</template>

<style lang="scss">
.nav__menu {
  display: flex;
  align-items: center;
  gap: 8px;
  border-right: 1px solid white;
  padding-right: 16px;
  margin-right: 16px;
}
</style>
