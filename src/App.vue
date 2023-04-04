<script setup>
import { provide, ref } from "vue";
import Navbar from "./components/Navbar/Navbar.vue";
import Sidebar from "./components/Sidebar/Sidebar.vue";
import Metric from "./components/Metric/Metric.vue";
import Table from "./components/Table/Table.vue";
import DetailSidebar from "./components/DetailSidebar/DetailSidebar.vue";

const dataGempa = ref();
const toggleDetailSidebar = ref(false);
const selectedData = ref();

async function getData() {
  // Check info gempa on local storage
  const dataGempaLocal = localStorage.getItem("data-gempa");
  if (dataGempaLocal) {
    dataGempa.value = JSON.parse(dataGempaLocal);
    return;
  }

  // Fetch API from BMKG
  const res = await fetch("/api");
  const finalData = await res.json();

  dataGempa.value = finalData.Infogempa.gempa;

  // Set to local storage
  localStorage.setItem("data-gempa", JSON.stringify(finalData.Infogempa.gempa));
}

getData();

// Props drilling
provide("dataGempa", dataGempa);
provide("toggleDetailSidebar", toggleDetailSidebar);
provide("selectedData", selectedData);
</script>

<template>
  <main class="container">
    <Sidebar />
    <div class="content">
      <Navbar title="Data Gempa" />
      <Metric />
      <Table />
    </div>
    <div
      v-if="toggleDetailSidebar"
      class="overlay"
      aria-hidden="false"
    >
      <DetailSidebar v-if="toggleDetailSidebar" />
    </div>
  </main>
</template>

<style lang="scss">
@keyframes overlayAni {
  from {
    background-color: rgba(51, 56, 57, 0);
  }
  to {
    background-color: rgba(51, 56, 57, 0.25);
  }
}

.overlay {
  position: fixed;
  inset: 0;
  background-color: rgba(51, 56, 57, 0.25);
  overflow-y: scroll;
  overflow-x: hidden;
  animation: overlayAni 1s ease;
}

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

.container {
  display: grid;
  grid-template-columns: 0.5fr 1.5fr;
}
</style>
