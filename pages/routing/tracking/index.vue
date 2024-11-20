<script setup lang="ts">
definePageMeta({
  layoutWrapperClasses: "layout-content-height-fixed",
  sidebarCollapsed: true,
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

</script>

<template>
  <VCard class="mb-6">
    <VCardText class="d-flex flex-wrap gap-4 px-3 py-3 tracking-bar">
      <VCardTitle>22 September 2024</VCardTitle>
      <VSpacer />
      <AppSelect
        placeholder="Select Branch/Depo"
        :items="['cabang 1', 'cabang 2', 'cabang 3']"
        clearable
        clear-icon="tabler-x"
      />
    </VCardText>

    <VDivider />
    <VCardItem class="px-0 py-0">
      <VRow>
        <VCol md="7" class="px-0">
          <div class="map-tracking">
          </div>
        </VCol>
        <VCol md="5" class="px-0">
          <!-- 👉 Table -->
          <VDataTable
            :items="items"
            key="items.id"
            item-value="id"
            :headers="headers"
            class="text-wrap text-body-2 routing-table overflow-auto"
            hide-default-footer
            density="compact"
            fixed-header
          >

          <!-- 👉 Action -->
        <template #item.actions="{ item }">
          <VBtn
            icon
            color="secondary"
            variant="outlined"
          >
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
        </VCol>
      </VRow>
    </VCardItem>
  </VCard>

  <VLayout class="fleet-app-layout">
    <VMain>
      <div class="h-100">
        <IconBtn
          class="d-lg-none navigation-toggle-btn rounded-sm"
          variant="elevated"
        >
          <VIcon icon="tabler-menu-2" />
        </IconBtn>
        <!-- 👉 Fleet map  -->
        <div id="mapContainer" class="basemap" />
      </div>
    </VMain>
  </VLayout>
</template>

<style lang="scss">
@use "@styles/variables/vuetify.scss";
@use "@core/scss/base/mixins.scss";

.fleet-app-layout {
  border-radius: vuetify.$card-border-radius;

  @include mixins.elevation(vuetify.$card-elevation);

  $sel-fleet-app-layout: &;

  @at-root {
    .skin--bordered {
      @include mixins.bordered-skin($sel-fleet-app-layout);
    }
  }
}

.navigation-toggle-btn {
  position: absolute;
  z-index: 1;
  inset-block-start: 1rem;
  inset-inline-start: 1rem;
}

.navigation-close-btn {
  position: absolute;
  z-index: 1;
  inset-block-start: 1rem;
  inset-inline-end: 1rem;
}

.basemap {
  block-size: 100%;
  inline-size: 100%;
}

.marker-focus {
  filter: drop-shadow(0 0 7px rgb(var(--v-theme-primary)));
}

.mapboxgl-ctrl-bottom-left,
.mapboxgl-ctrl-bottom-right {
  display: none;
}

.fleet-navigation-drawer {
  .v-timeline .v-timeline-divider__dot .v-timeline-divider__inner-dot {
    box-shadow: none;
  }
}

.fleet-timeline {
  &.v-timeline .v-timeline-item:not(:last-child) {
    .v-timeline-item__body {
      margin-block-end: 0.25rem;
    }
  }
}

/* stylelint-disable-next-line selector-id-pattern */
#mapContainer {
  block-size: 100vh !important;
}

.map-tracking {
  width: 100%;
  // height: 100%;
  background: #000000;
  block-size: 90vh !important;
}

.tracking-bar {
  position: sticky;
  top: 0;
  background: #fff;
  z-index: 10;
}
</style>
