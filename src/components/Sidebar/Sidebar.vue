<script setup>
import SidebarMenu from "./SidebarMenu.vue";
import SidebarMenuItem from "./SidebarMenuItem.vue";
import IconDashboard from "../icons/IconDashboard.vue";
import IconClipboardWhite from "../icons/IconClipboardWhite.vue";
import IconBarChart from "../icons/IconBarChart.vue";
import IconMap from "../icons/IconMap.vue";
import IconSupport from "../icons/IconSupport.vue";
import IconPhone from "../icons/IconPhone.vue";
</script>

<template>
  <div class="sidebar">
    <div class="sidebar--top">
      <div class="sidebar__brand">
        <img
          src="@/assets/logo.svg"
          alt=""
        />
        <h1>Logo</h1>
      </div>
      <SidebarMenu>
        <SidebarMenuItem title="Dashboard">
          <IconDashboard />
        </SidebarMenuItem>
        <SidebarMenuItem
          title="Data Gempa"
          :isActive="true"
        >
          <IconClipboardWhite />
        </SidebarMenuItem>
        <SidebarMenuItem title="Analisis">
          <IconBarChart />
        </SidebarMenuItem>
        <SidebarMenuItem title="Peta Wilayah">
          <IconMap />
        </SidebarMenuItem>
      </SidebarMenu>
    </div>
    <div class="sidebar--bottom">
      <SidebarMenu>
        <SidebarMenuItem title="Support">
          <IconSupport />
        </SidebarMenuItem>
        <SidebarMenuItem title="Contact Us">
          <IconPhone />
        </SidebarMenuItem>
      </SidebarMenu>
    </div>
  </div>
</template>

<style lang="scss">
.sidebar {
  background-color: #fff;
  box-shadow: 0px 4px 30px rgba(26, 28, 33, 0.08);
  height: 1100px;
  margin: 16px;
  padding: 16px;
  border-radius: 16px;
  display: flex;
  justify-content: space-between;
  flex-direction: column;

  &__brand {
    padding: 8px calc(24px - 16px) 16px;
    display: flex;
    align-items: center;
    gap: 12px;

    h1 {
      font-weight: 700;
      font-size: 18px;
      color: #333843;
    }
  }
}
</style>
