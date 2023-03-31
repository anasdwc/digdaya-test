<script setup>
import { inject, onBeforeMount, onMounted } from "vue";
import Pagination from "./Pagination.vue";

const dataGempa = inject("dataGempa");

// const descDataGempaByDate = computed(() => {
//   return dataGempa.value.sort((date1, date2) => {
//     let date1Formatted = new Date(date1.DateTime);
//     let date2Formatted = new Date(date2.DateTime);
//     return date1Formatted.getTime() - date2Formatted.getTime();
//   });
// });
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
      <tr v-for="data in dataGempa">
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
