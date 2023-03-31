<script setup>
import MetricCard from "./MetricCard.vue";
import IconClipboardPurple from "../icons/IconClipboardPurple.vue";
import IconTop from "../icons/IconTop.vue";
import IconBottom from "../icons/IconBottom.vue";
import IconCalendar from "../icons/IconCalendar.vue";
</script>

<template>
  <div class="metric">
    <div class="metric__list">
      <MetricCard
        title="15"
        description="Total Data"
      >
        <IconClipboardPurple />
      </MetricCard>
      <MetricCard
        title="2.4 Mag"
        description="Tertinggi"
      >
        <IconTop />
      </MetricCard>
      <MetricCard
        title="4.5 Km"
        description="Rata-rata Kedalaman"
      >
        <IconBottom />
      </MetricCard>
      <MetricCard
        title="28 Mar 23"
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
