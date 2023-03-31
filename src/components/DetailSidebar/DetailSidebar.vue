<script setup>
import { inject } from "vue";

const toggleDetailSidebar = inject("toggleDetailSidebar");

function closeSidebar() {
  toggleDetailSidebar.value = false;
}
</script>

<template>
  <div
    v-if="toggleDetailSidebar"
    class="detail"
  >
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
        <p>28 Maret 2023</p>
      </div>
      <div class="detail__item">
        <h4>Jam</h4>
        <p>03:44 WIB</p>
      </div>
      <div class="detail__item">
        <h4>Date Time</h4>
        <p>2023-03-27T17 : 03:44+00:00</p>
      </div>
      <div class="detail__item">
        <h4>Koordinat</h4>
        <p>3.24, 97.92</p>
      </div>
      <div class="detail__item">
        <h4>Lintang</h4>
        <p>3.24 LU</p>
      </div>
      <div class="detail__item">
        <h4>Bujur</h4>
        <p>97.92 BT</p>
      </div>
      <div class="detail__item">
        <h4>Magnitudo</h4>
        <p>2.4</p>
      </div>
      <div class="detail__item">
        <h4>Kedalaman</h4>
        <p>4 Km</p>
      </div>
      <div class="detail__item">
        <h4>Wilayah</h4>
        <p>
          Pusat gempa berada di darat 29 km Tenggara Kutacane - Kab. Aceh
          Tenggara
        </p>
      </div>
      <div class="detail__item">
        <h4>Dirasakan</h4>
        <p>II Pasie Raja, Kab. Aceh Selatan</p>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.detail {
  position: absolute;
  background-color: #fff;
  right: 0;
  padding: 24px;
  width: 400px;

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
