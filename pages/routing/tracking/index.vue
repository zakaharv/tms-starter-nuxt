<script setup lang="ts">
definePageMeta({
  layoutWrapperClasses: "layout-content-height-fixed",
});

//👉 - Dummy Interface Data
interface Items {
  id: number;
  tripId: string;
  vehicle: string;
  vehicleNumber: string;
  driver: string;
  sales: string;
  vol: number;
  kg: number;
  km: number;
  dps: number;
  total: string;
  lock: boolean;
  status: string;
}

//👉 - Dummy Object Data
const items = ref<Items[]>([
  {
    id: 1,
    tripId: "V1",
    vehicle: "GM",
    vehicleNumber: "AG1234YT",
    driver: "Jhon Buffed",
    sales: "480 jt",
    vol: 295,
    kg: 7476,
    km: 125,
    dps: 11,
    total: "9h 10m",
    lock: true,
    status: "new",
  },
  {
    id: 2,
    tripId: "V2",
    vehicle: "Motorcycle",
    vehicleNumber: "AG1234YT",
    driver: "Jhon Buffed",
    sales: "480 rb",
    vol: 295,
    kg: 7476,
    km: 125,
    dps: 11,
    total: "9h 10m",
    lock: false,
    status: "confirmed",
  },
]);

// 👉 Headers
const headers = [
  { title: "#", key: "actions", sortable: false },
  { title: "Vehicle", key: "vehicle" },
  { title: "Sales", key: "sales" },
  { title: "Total", key: "total" },
];

const menu = ref(false);
</script>

<template>
  <VCard class="mb-6" style="height: 100%; overflow: hidden">
    <VCardText class="d-flex flex-wrap gap-4 px-3 py-3 tracking-bar">
      <VCardTitle>22 September 2024</VCardTitle>
      <VSpacer />
      <VRow no-gutters>
        <VCol md="2" class="d-flex align-items-center"> <label
              class="v-label text-body-2 text-high-emphasis"
            >Branch/Depo</label></VCol>
        <VCol md="10"><AppSelect
        placeholder="Select Branch/Depo"
        :items="['cabang 1', 'cabang 2', 'cabang 3']"
        clearable
        clear-icon="tabler-x"
      /></VCol>
      </VRow>
    </VCardText>

    <VDivider />
    <VRow style="width: 100%; height: calc(100% - 70px); margin: 0px">
      <VCol cols="12" md="7" class="px-0 py-0" >
        <div class="map-tracking">
          <!-- 👉 Guide -->
          <div class="guide-status">
            <VIcon icon="tabler-current-location" size="16" />
            <div class="text-body-2">
              You’re viewing
              <span style="color: #000">V1 • GM • AG1234Y • Jhon Buffed</span>
            </div>
          </div>
          <!-- 👉 Example Dot with Popover -->
          <VMenu
            v-model="menu"
            :close-on-content-click="false"
            location="top center"
          >
            <template v-slot:activator="{ props }">
              <VBtn
                color="primary"
                rounded
                variant="outlined"
                size="32"
                v-bind="props"
                style="background-color: #fff; border-width: 3px"
              >
                1
              </VBtn>
            </template>

            <VCard min-width="300">
              <VCardText class="px-3 py-3 d-flex">
                <h5 style="font-size: 18px; line-height: 1.7rem">
                  48/01/035822
                </h5>
                <VSpacer />
                <DialogCloseBtn @click="menu = !menu" />
              </VCardText>

              <VDivider></VDivider>

              <VList>
                <VListItem>
                  <p class="text-body-2 mb-0">Customer Sequence</p>
                  <p class="text-body-1 font-weight-bold mb-0">8</p>
                </VListItem>
                <VListItem>
                  <p class="text-body-2 mb-0">Customer Name</p>
                  <p class="text-body-1 font-weight-bold mb-0">
                    Toko Maju Jaya Abadi
                  </p>
                </VListItem>
                <VListItem>
                  <p class="text-body-2 mb-0">Address</p>
                  <p class="text-body-1 font-weight-bold mb-0">
                    Jl ABC 123 qwert, 56 57
                  </p>
                </VListItem>
              </VList>

              <VCardActions>
                <VBtn
                  variant="outlined"
                  color="error"
                  size="small"
                  @click="menu = false"
                  class="w-100"
                >
                  UNASSIGNED
                </VBtn>
              </VCardActions>
            </VCard>
          </VMenu>
        </div>
      </VCol>
      <VCol cols="12" md="5" class="px-0 py-0">
        <div style="height: calc(100% - 70px); width: 100%; overflow: scroll">
          <!-- 👉 Table -->
          <VDataTable
            :items="items"
            key="items.id"
            item-value="id"
            :headers="headers"
            class="text-wrap text-body-2 routing-table overflow-auto"
            hide-default-footer
            density="compact"
          >
            <!-- 👉 Action -->
            <template #item.actions>
              <VBtn icon color="secondary" variant="outlined" size="32">
                <VIcon size="16" icon="tabler-current-location" />
                <VTooltip location="top" activator="parent"> Track </VTooltip>
              </VBtn>
            </template>
            <!-- 👉 Vehicle -->
            <template #item.vehicle="{ item }">
              <div class="vehicle-set">
                <div class="trip-title">
                  <VChip
                    class="text-body-1 font-weight-bold px-0"
                    color="success"
                    variant="text"
                    >V1</VChip
                  >
                  <span class="trip-status">
                    <span>{{ item.status }}</span>
                  </span>
                </div>
              </div>
              <div class="body-text-2 vehicle-info">
                <span> {{ item.vehicle }} </span> • {{ item.vehicleNumber }}
              </div>
              <div class="body-text-2">{{ item.driver }}</div>
            </template>

            <!-- 👉 Sales -->
            <template #item.sales="{ item }"> Rp{{ item.sales }} </template>

            <!-- 👉 Total -->
            <template #item.total="{ item }">
              <div class="text-body-2">{{ item.total }} • {{ item.km }} km</div>
              <div class="d-flex align-items-center gap-1">
                <VChip size="small" color="error" variant="outlined">
                  {{ item.vol }} Vol
                </VChip>
                <VChip size="small" color="warning" variant="outlined">
                  {{ item.kg }} Kg
                </VChip>
                <VChip size="small" color="success" variant="outlined">
                  {{ item.vol }} Point
                  <VTooltip open-delay="500" location="top" activator="parent">
                    <span>View Detail</span>
                  </VTooltip>
                </VChip>
              </div>
            </template>
          </VDataTable>
        </div>
      </VCol>
    </VRow>
  </VCard>
</template>

<style lang="scss">


.map-tracking {
  width: 100%;
  height: 100%;
  // height: 100%;
  background: #000000;
  position: relative;
}



.guide-status {
  background-color: #fff;
  display: inline-flex;
  padding: 10px 16px;
  justify-content: center;
  align-items: center;
  gap: 6px;
  border-radius: 6px;
  box-shadow: 0px 4px 18px 0px rgba(47, 43, 61, 0.16);
  position: absolute;
  top: 10px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 99;
}
</style>
