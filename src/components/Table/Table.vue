<script setup>
import { inject, onBeforeMount, onMounted, provide, ref } from "vue";
import Pagination from "./Pagination.vue";
import { computed } from "@vue/reactivity";

const dataGempa = inject("dataGempa");
const toggleDetailSidebar = inject("toggleDetailSidebar");
const selectedData = inject("selectedData");

const rowsPerPage = ref(10);
const startRow = ref(0);
const pageDataGempa = computed(() => {
  return dataGempa.value.slice(
    startRow.value,
    startRow.value + rowsPerPage.value
  );
});

// const descDataGempaByDate = computed(() => {
//   return dataGempa.value.sort((date1, date2) => {
//     let date1Formatted = new Date(date1.DateTime);
//     let date2Formatted = new Date(date2.DateTime);
//     return date1Formatted.getTime() - date2Formatted.getTime();
//   });
// });

function handleClick(coord) {
  const filterData = dataGempa.value.filter(
    (data) => coord == data.Coordinates
  );

  selectedData.value = filterData;
  toggleDetailSidebar.value = true;
}

provide("rowsPerPage", rowsPerPage);
provide("startRow", startRow);
</script>

<template>
  <table class="table">
    <thead class="table__header">
      <tr>
        <th>tanggal</th>
        <th>jam</th>
        <th>coordinates</th>
        <th>magnitudo</th>
        <th>kedalaman</th>
        <th>wilayah</th>
      </tr>
    </thead>
    <tbody class="table__body">
      <tr
        v-for="(data, index) in pageDataGempa"
        @click="() => handleClick(data.Coordinates)"
      >
        <template v-if="index < rowsPerPage">
          <td>{{ data.Tanggal }}</td>
          <td>
            {{ data.Jam.split(" ")[0].split(":").slice(0, 2).join(":") }} WIB
          </td>
          <td>{{ data.Coordinates.split(",").join(", ") }}</td>
          <td>{{ data.Magnitude }} Mag</td>
          <td>{{ data.Kedalaman }}</td>
          <td>
            {{
              data.Wilayah.split(/(\d+)/)
                .slice(-1)[0]
                .split("km")
                .slice(-1)[0]
                .trim()
            }}
          </td>
        </template>
      </tr>
    </tbody>
  </table>
  <Pagination />
</template>

<style lang="scss">
.table {
  background-color: white;
  margin: 24px 0;
  width: 100%;
  border-radius: 8px;
  box-shadow: 0px 4px 30px rgba(26, 28, 33, 0.08);

  th,
  td {
    font-size: 14px;
    letter-spacing: 0.005em;
  }

  tr:hover {
    background-color: #f3f0ff;
    cursor: pointer;
  }

  th {
    text-transform: uppercase;
    padding: 18px 24px;
    border-bottom: 1px solid #e0e2e7;
    text-align: left;
    color: #858d9d;
    font-weight: 600;
  }

  td {
    padding: 26px 24px;
    font-weight: 500;
    color: #333843;
  }
}
</style>
