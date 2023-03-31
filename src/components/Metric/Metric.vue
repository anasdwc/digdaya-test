<script setup>
import MetricCard from "./MetricCard.vue";
import IconClipboardPurple from "../icons/IconClipboardPurple.vue";
import IconTop from "../icons/IconTop.vue";
import IconBottom from "../icons/IconBottom.vue";
import IconCalendar from "../icons/IconCalendar.vue";
import { computed, inject, ref } from "vue";

const dataGempa = inject("dataGempa");

const highestMag = computed(() => {
  return dataGempa.value.reduce((highestAcc, data) => {
    let magnitude = parseFloat(data.Magnitude);
    return Math.max(highestAcc, magnitude);
  }, -Infinity);
});

const avgKedalaman = computed(() => {
  let totalKedalaman = 0;

  dataGempa.value.forEach((data) => {
    let kedalaman = parseInt(data.Kedalaman);
    totalKedalaman += kedalaman;
  });

  return (totalKedalaman / dataGempa.value.length).toFixed(1);
});

const dataTerbaru = computed(() => {
  let terbaru = new Date();

  dataGempa.value.forEach((data) => {
    let dateFormatted = new Date(data.DateTime);

    if (dateFormatted.getTime() > terbaru.getTime()) {
      terbaru = dateFormatted;
    }
  });

  return terbaru.toLocaleString("id-ID", {
    day: "2-digit",
    month: "short",
    year: "2-digit",
  });
});
</script>

<template>
  <div class="metric">
    <div class="metric__list">
      <MetricCard
        :title="dataGempa.length"
        description="Total Data"
      >
        <IconClipboardPurple />
      </MetricCard>
      <MetricCard
        :title="`${highestMag} Mag`"
        description="Tertinggi"
      >
        <IconTop />
      </MetricCard>
      <MetricCard
        :title="`${avgKedalaman} Km`"
        description="Rata-rata Kedalaman"
      >
        <IconBottom />
      </MetricCard>
      <MetricCard
        :title="dataTerbaru"
        description="Terbaru"
      >
        <IconCalendar />
      </MetricCard>
    </div>
  </div>
</template>

<style lang="scss">
.metric {
  margin-top: 24px;

  &__list {
    display: flex;
    gap: 24px;
  }
}
</style>
