<script setup>
import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "./components/HelloWorld.vue";
import Navbar from "./components/Navbar/Navbar.vue";
import Sidebar from "./components/Sidebar/Sidebar.vue";
import Metric from "./components/Metric/Metric.vue";
</script>

<template>
  <div class="decoration"></div>
  <main class="container">
    <Sidebar />
    <div class="content">
      <Navbar title="Data Gempa" />
      <Metric />
    </div>
  </main>
  <!-- <header>
    <img
      alt="Vue logo"
      class="logo"
      src="@/assets/logo.svg"
      width="125"
      height="125"
    />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header> -->

  <!-- <RouterView /> -->
</template>

<style lang="scss">
.metric {
  margin-top: 24px;

  &__list {
    display: flex;
    gap: 24px;
  }
}

.content {
  padding: 24px;
}
.decoration {
  position: absolute;
  width: 100%;
  height: 152px;
  background-color: #643dff;
  z-index: -1;
}
.container {
  display: grid;
  grid-template-columns: 0.5fr 1.5fr;
}
</style>
