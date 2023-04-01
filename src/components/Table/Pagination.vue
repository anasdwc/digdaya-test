<script setup>
import { inject, provide, ref } from "vue";
import PaginationButton from "./PaginationButton.vue";
import { computed } from "@vue/reactivity";

const rowsPerPage = inject("rowsPerPage");
const startRow = inject("startRow");
const dataGempa = inject("dataGempa");
const positionPage = ref(1);

const lengthPage = computed(() => {
  return Math.ceil(dataGempa.value.length / rowsPerPage.value);
});

function handleInputLimit(e) {
  let num = parseInt(e.target.value);

  if (num > 15) {
    rowsPerPage.value = 15;
    return;
  }

  rowsPerPage.value = num;
  startRow.value = 0;
  positionPage.value = 1;
}

function movePages(amount, isButton) {
  // Jika angka, maka dapat move page dalam jumlah yg banyak
  let newAmount = amount - positionPage.value;

  // Jika button, maka stepnya satu
  if (isButton) {
    newAmount = amount >= positionPage.value ? 1 : -1;
  }

  let newStartRow = startRow.value + newAmount * rowsPerPage.value;
  if (newStartRow >= 0 && newStartRow < dataGempa.value.length) {
    startRow.value = newStartRow;
    positionPage.value += newAmount;
  }
}

provide("positionPage", positionPage);
</script>

<template>
  <div class="pagination">
    <div class="pagination__detail">
      <p>
        <span>Show</span>
        <input
          type="number"
          placeholder="10"
          :value="rowsPerPage"
          @change="handleInputLimit"
        />
        <span>
          from
          <span class="total-data">15</span>
        </span>
      </p>
    </div>
    <div class="pagination__nav">
      <PaginationButton
        isButton
        @move-page="(page, isButton) => movePages(-Infinity, isButton)"
      >
        <template #icon>
          <img
            src="@/assets/left.svg"
            alt=""
          />
        </template>
      </PaginationButton>
      <template v-for="(val, idx) in lengthPage">
        <PaginationButton
          :page="idx + 1"
          @move-page="(page, isButton) => movePages(page, isButton)"
        />
      </template>
      <PaginationButton
        isButton
        @move-page="(page, isButton) => movePages(Infinity, isButton)"
      >
        <template #icon>
          <img
            src="@/assets/right.svg"
            alt=""
          />
        </template>
      </PaginationButton>
    </div>
  </div>
</template>

<style lang="scss">
.pagination {
  display: flex;
  justify-content: space-between;
  margin: 24px 0;

  button {
    border: none;
    cursor: pointer;
  }

  &__detail {
    p {
      display: flex;
      align-items: center;
      gap: 8px;
      font-size: 16px;
    }

    .total-data {
      font-weight: 500;
    }

    input {
      border: 1px solid #e0e2e7;
      padding: 4px 8px;
      width: 36px;
      height: 36px;
      border-radius: 8px;

      line-height: 19.6px;
      font-size: 14px;
      color: #333843;
      font-weight: 500;
    }
  }

  &__nav {
    display: flex;
    gap: 8px;

    &__button,
    &__number {
      padding: 8px;
    }

    &__number {
      padding: 8px;
      width: 36px;
      height: auto;
      border-radius: 8px;
      display: flex;
      justify-content: center;
      align-items: center;
      line-height: 15.84px;

      color: #667085;
      font-size: 12px;
      font-weight: 600;

      &--active {
        background-color: #643dff;
        color: white;
      }
    }

    &__button {
      background-color: #f0ecff;
      border-radius: 8px;
    }
  }
}
</style>
