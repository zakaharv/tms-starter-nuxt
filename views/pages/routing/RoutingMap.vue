<script setup lang="ts">
import ViewMissingRoute from './dialogs/ViewMissingRoute.vue';

const fav = ref(true);
const menu = ref(false);
const message = ref(false);
const hints = ref(true);

const isViewMissingRouteVisible = ref(false);
</script>

<template>
  <!-- ➡️ Remove this -->
  <div class="text-white">Mapnya nanti disini</div>

  <!-- 👉 Example Dot with Popover -->
  <VMenu v-model="menu" :close-on-content-click="false" location="top center">
    <template v-slot:activator="{ props }">
      <VBtn color="primary" rounded variant="outlined" size="32" v-bind="props"
        style="background-color: #fff; border-width: 3px">
        1
      </VBtn>
    </template>

    <VCard min-width="300">
      <VCardText class="px-3 py-3 d-flex">
        <h5 style="font-size: 18px; line-height: 1.7rem">48/01/035822</h5>
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
          <p class="text-body-1 font-weight-bold mb-0">Toko Maju Jaya Abadi</p>
        </VListItem>
        <VListItem>
          <p class="text-body-2 mb-0">Address</p>
          <p class="text-body-1 font-weight-bold mb-0">
            Jl ABC 123 qwert, 56 57
          </p>
        </VListItem>
      </VList>

      <VCardActions>
        <VBtn variant="outlined" color="error" size="small" @click="menu = false" class="w-100">
          UNASSIGNED
        </VBtn>
      </VCardActions>
    </VCard>
  </VMenu>

  <div class="missing-route-wrapper">
    <div class="topbar-overview-card">
      <div>
        <label class="text-body-2 text-white"> Drop Point</label>
        <div style="color: #ffc58e; font-weight: 700; line-height: 1.2rem">
          15
        </div>
      </div>
    </div>
    <div class="topbar-overview-card" style="background-color: #bf393d;">
      <div>
        <label class="text-body-2 text-white"> Missing Route</label>
        <div class="missing-route-view">
          <div class="missing-route-visible">
            <VBtn icon="tabler-eye" variant="text" color="white" size="24" />
            <div style="color: #ffc58e; font-weight: 700; line-height: 1.2rem">
              4
            </div>

          </div>
          <VBtn icon="tabler-chevron-right" variant="text" color="white" size="20"
            @click="isViewMissingRouteVisible = true" />
        </div>
      </div>
    </div>
  </div>

  <ViewMissingRoute v-model:isDialogVisible="isViewMissingRouteVisible"></ViewMissingRoute>
</template>

<style>
.missing-route-view {
  display: flex;
  justify-content: space-between;
}

.missing-route-wrapper {
  position: absolute;
  top: 16px;
  right: 16px;
  display: flex;
  gap: 8px;
}

.missing-route-visible {
  display: flex;
  align-items: center;
  gap: 4px;
}
</style>
