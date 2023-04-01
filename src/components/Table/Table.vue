<script setup>
import { inject, onUpdated, provide, ref } from "vue";
import Pagination from "./Pagination.vue";
import { computed } from "@vue/reactivity";
import SortButton from "./SortButton.vue";

const dataGempa = inject("dataGempa");
const toggleDetailSidebar = inject("toggleDetailSidebar");
const selectedData = inject("selectedData");

const rowsPerPage = ref(10);
const startRow = ref(0);
const nowSortBy = ref("DateTime");
const sortAsc = ref(true);

const pageDataGempa = computed(() => {
  return dataGempa.value.slice(
    startRow.value,
    startRow.value + rowsPerPage.value
  );
});

function sortGempaByDate(asc) {
  nowSortBy.value = "DateTime";

  if (asc) {
    return dataGempa.value.sort((date1, date2) => {
      let date1Formatted = new Date(date1.DateTime);
      let date2Formatted = new Date(date2.DateTime);
      sortAsc.value = false;
      return date1Formatted.getTime() - date2Formatted.getTime();
    });
  }

  return dataGempa.value.sort((date1, date2) => {
    let date1Formatted = new Date(date1.DateTime);
    let date2Formatted = new Date(date2.DateTime);
    sortAsc.value = true;
    return date2Formatted.getTime() - date1Formatted.getTime();
  });
}

function sortGempaNumber(asc, key) {
  nowSortBy.value = key;

  if (asc) {
    return dataGempa.value.sort((data1, data2) => {
      let data1Formatted = parseFloat(data1[key]);
      let data2Formatted = parseFloat(data2[key]);
      sortAsc.value = false;
      return data2Formatted - data1Formatted;
    });
  }

  return dataGempa.value.sort((data1, data2) => {
    let data1Formatted = parseFloat(data1[key]);
    let data2Formatted = parseFloat(data2[key]);
    sortAsc.value = true;
    return data1Formatted - data2Formatted;
  });
}

function sortGempa(asc, key) {
  if (key == "DateTime") {
    sortGempaByDate(asc);
    return;
  }

  sortGempaNumber(asc, key);
  return;
}

function handleClick(e, datetime) {
  const filterData = dataGempa.value.filter(
    (data) => datetime == data.DateTime
  );

  e.target.parentNode.classList.add("active-row");

  selectedData.value = filterData;
  toggleDetailSidebar.value = true;
}

provide("rowsPerPage", rowsPerPage);
provide("startRow", startRow);
provide("sortAsc", sortAsc);
provide("nowSortBy", nowSortBy);
</script>

<template>
  <table class="table">
    <thead class="table__header">
      <tr>
        <th>
          <div>
            <p>tanggal</p>
            <SortButton
              ele="DateTime"
              @sort-by="(key) => sortGempa(sortAsc, key)"
            />
          </div>
        </th>
        <th><p>jam</p></th>
        <th><p>coordinates</p></th>
        <th>
          <div>
            <p>magnitudo</p>
            <SortButton
              ele="Magnitude"
              @sort-by="(key) => sortGempa(sortAsc, key)"
            />
          </div>
        </th>
        <th>
          <div>
            <p>kedalaman</p>
            <SortButton
              ele="Kedalaman"
              @sort-by="(key) => sortGempa(sortAsc, key)"
            />
          </div>
        </th>
        <th>
          <p>wilayah</p>
        </th>
      </tr>
    </thead>
    <tbody class="table__body">
      <tr
        v-for="(data, index) in pageDataGempa"
        @click="(e) => handleClick(e, data.DateTime)"
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

  tr:hover td {
    background-color: #f3f0ff;
    cursor: pointer;
  }

  tr.active-row td {
    background-color: #f3f0ff;
  }

  th {
    text-transform: uppercase;
    padding: 18px 24px;
    border-bottom: 1px solid #e0e2e7;
    min-width: 120px;

    & > div {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    p {
      text-align: left;
      color: #858d9d;
      font-weight: 600;
    }
  }

  td {
    padding: 26px 24px;
    font-weight: 500;
    color: #333843;
    vertical-align: middle;
  }
}
</style>
