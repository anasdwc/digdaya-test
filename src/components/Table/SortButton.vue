<script setup>
import { inject } from "vue";
import IconSort from "../icons/IconSort.vue";

const props = defineProps({
  ele: {
    type: String,
  },
});

const sortAsc = inject("sortAsc");
const nowSortBy = inject("nowSortBy");

const emit = defineEmits(["sort-by"]);
</script>

<template>
  <button
    class="icon-sort"
    @click="emit('sort-by', props.ele)"
  >
    <IconSort
      class="rotate-icon"
      :class="{
        'icon-sort--active': !sortAsc && nowSortBy == props.ele,
      }"
    />
    <IconSort
      :class="{
        'icon-sort--active': sortAsc && nowSortBy == props.ele,
      }"
    />
  </button>
</template>

<style lang="scss">
.icon-sort {
  display: flex;
  flex-direction: column;
  gap: 3px;

  &--active path {
    fill: #333843;
  }

  .rotate-icon {
    transform: rotate(180deg);
  }

  cursor: pointer;
  background-color: transparent;
  border: none;
}
</style>
