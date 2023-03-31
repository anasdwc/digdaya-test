<script setup>
import NavbarMenu from "./NavbarMenu.vue";
import NavbarAccount from "./NavbarAccount.vue";

defineProps({
  title: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <nav class="nav">
    <h2>{{ title }}</h2>
    <div class="nav__list">
      <NavbarMenu />
      <NavbarAccount />
    </div>
  </nav>
</template>

<style lang="scss">
.nav {
  background-color: #643dff;
  display: flex;
  align-items: center;
  justify-content: space-between;
  color: white;
  padding: 24px;

  h2 {
    font-size: 24px;
    font-weight: 600;
  }

  p {
    color: white;
  }

  &__list {
    display: flex;
    align-items: center;
  }
}
</style>
