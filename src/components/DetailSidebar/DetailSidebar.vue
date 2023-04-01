<script setup>
import { inject, onBeforeMount, onMounted, onUnmounted } from "vue";

const toggleDetailSidebar = inject("toggleDetailSidebar");
const selectedData = inject("selectedData");

let data = null;

onBeforeMount(() => {
  data = selectedData.value[0];
});

onMounted(() => {
  document.body.classList.add("noscroll");
});

onUnmounted(() => {
  document.body.classList.remove("noscroll");
});

function closeSidebar() {
  toggleDetailSidebar.value = false;
}
</script>

<template>
  <div class="detail">
    <div class="detail__header">
      <h3>Detail</h3>
      <button @click="closeSidebar">
        <img
          src="@/assets/close.svg"
          alt=""
        />
      </button>
    </div>
    <div class="detail__list">
      <div class="detail__item">
        <h4>Tanggal</h4>
        <p>{{ data.Tanggal }}</p>
      </div>
      <div class="detail__item">
        <h4>Jam</h4>
        <p>{{ data.Jam.split(" ")[0].split(":").slice(0, 2).join(":") }} WIB</p>
      </div>
      <div class="detail__item">
        <h4>Date Time</h4>
        <p>{{ data.DateTime }}</p>
      </div>
      <div class="detail__item">
        <h4>Koordinat</h4>
        <p>{{ data.Coordinates.split(",").join(", ") }}</p>
      </div>
      <div class="detail__item">
        <h4>Lintang</h4>
        <p>{{ data.Lintang }}</p>
      </div>
      <div class="detail__item">
        <h4>Bujur</h4>
        <p>{{ data.Bujur }}</p>
      </div>
      <div class="detail__item">
        <h4>Magnitudo</h4>
        <p>{{ data.Magnitude }}</p>
      </div>
      <div class="detail__item">
        <h4>Kedalaman</h4>
        <p>{{ data.Kedalaman }}</p>
      </div>
      <div class="detail__item">
        <h4>Wilayah</h4>
        <p>
          {{ data.Wilayah }}
        </p>
      </div>
      <div class="detail__item">
        <h4>Dirasakan</h4>
        <p>{{ data.Dirasakan }}</p>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@keyframes slideIn {
  from {
    opacity: 1;
    transform: translate(400px);
  }
  to {
    opacity: 1;
    transform: translate(0);
  }
}

.detail {
  position: absolute;
  background-color: #fff;
  right: 0;
  padding: 24px;
  width: 400px;
  height: 1000px;
  animation: slideIn 0.5s ease;

  &__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-bottom: 20px;
    border-bottom: 1px solid #e0e2e7;

    button {
      border: none;
      background-color: transparent;
      cursor: pointer;
      width: 20px;
      height: 20px;
      padding: 0;
    }

    h3 {
      font-weight: 600;
      font-size: 20px;
    }
  }

  &__list {
    margin-top: 20px;
    display: flex;
    gap: 18px;
    flex-direction: column;
  }

  &__item {
    p,
    h4 {
      font-size: 14px;
      font-weight: 500;
      line-height: 19.6px;
    }

    p {
      color: #333843;
    }

    h4 {
      color: #858d9d;
      margin-bottom: 8px;
    }
  }
}
</style>
