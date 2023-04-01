<script setup>
import { computed } from "@vue/reactivity";
import { inject } from "vue";

const props = defineProps({
  page: {
    type: Number,
  },
  isButton: {
    type: Boolean,
  },
});

const emit = defineEmits(["move-page"]);

const positionPage = inject("positionPage");
const isActivePosition = computed(() => positionPage.value == props.page);
</script>

<template>
  <button
    @click="emit('move-page', props.page, props.isButton)"
    class="pagination__nav__number"
    :class="{
      'pagination__nav__number--active': isActivePosition,
      pagination__nav__button: isButton,
    }"
  >
    {{ page }}
    <slot name="icon"></slot>
  </button>
</template>
