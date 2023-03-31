<script setup>
import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "./components/HelloWorld.vue";
import { provide, ref } from "vue";
import { computed } from "@vue/reactivity";
import Navbar from "./components/Navbar/Navbar.vue";
import Sidebar from "./components/Sidebar/Sidebar.vue";
import Metric from "./components/Metric/Metric.vue";
import Table from "./components/Table/Table.vue";

const dataGempa = ref();

// TODO: Add limit and function to sort data

async function getData() {
  // Check info gempa on local storage
  const dataGempaLocal = localStorage.getItem("data-gempa");
  if (dataGempaLocal) {
    dataGempa.value = JSON.parse(dataGempaLocal);
    return;
  }

  // Fetch API from BMKG
  const res = await fetch("http://localhost:5173/api");
  const finalData = await res.json();

  dataGempa.value = finalData.Infogempa.gempa;

  // Set to local storage
  localStorage.setItem("data-gempa", JSON.stringify(finalData.Infogempa.gempa));
}

getData();

// Props drilling
provide("dataGempa", dataGempa);
</script>

<template>
  <div class="decoration"></div>
  <main class="container">
    <Sidebar />
    <div class="content">
      <Navbar title="Data Gempa" />
      <Metric />
      <Table />
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
