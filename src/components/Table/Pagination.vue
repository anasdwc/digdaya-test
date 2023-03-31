<script setup></script>

<template>
  <div class="pagination">
    <div class="pagination__detail">
      <p>
        <span>Show</span>
        <input
          type="text"
          placeholder="10"
          value="10"
        />
        <span>
          from
          <span class="total-data">15</span>
        </span>
      </p>
    </div>
    <div class="pagination__nav">
      <div class="pagination__nav__button pagination__nav__button--prev">
        <img
          src="@/assets/left.svg"
          alt=""
        />
      </div>
      <div class="pagination__nav__number pagination__nav__number--active">
        1
      </div>
      <div class="pagination__nav__number">2</div>
      <div class="pagination__nav__button pagination__nav__button--next">
        <img
          src="@/assets/right.svg"
          alt=""
        />
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.pagination {
  display: flex;
  justify-content: space-between;
  margin: 24px 0;

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
