<script setup lang="ts">
import AddEditOrderDialog from "./AddEditOrderDialog.vue";

//👉 - Dummy Interface Data
interface Items {
  id: number;
  invoice: string;
  batch: string;
  batchDate: string;
  customer: string;
  invDate: string;
  deliveryDate: string;
  amount: number;
  actual: number;
  isactive: boolean;
  reason: string;
  orderStatus: string;
  totalProduct: number;
  totalDiscTrx: number;
  totalDisc: number;
  totalPay: number;
  totalProductAct: number;
  totalDiscTrxAct: number;
  totalDiscAct: number;
  totalPayAct: number;
  totalCollect: number;
  totalPrint: number;
  createdat: string;
  createdby: string;
  updatedat: string;
  updatedby: string;
  products: Details[];
}

interface Details {
  id: number;
  code: string;
  name: string;
  price: number;
  qty: number;
  qtyactual: number;
  disc1: number;
  discactual1: number;
  disc2: number;
  discactual2: number;
  disc3: number;
  discactual3: number;
  disc4: number;
  discactual4: number;
}

const isAddEditOrderDialogVisible = ref(false);
const isDetailOrderDialogVisible = ref(false);

//👉 - Dummy Object Data
const items = ref<Items[]>([
  {
    id: 1,
    invoice: "INV12345",
    batch: "BATCH-1",
    batchDate: "20/20/2020",
    customer: "Toko Maju Jaya Abadi",
    invDate: "20/20/2020",
    deliveryDate: "20/20/2020",
    amount: 12000,
    actual: 12000,
    isactive: true,
    reason: "lorem ipsum",
    orderStatus: "ON DELIVERY",
    totalProduct: 12,
    totalDiscTrx: 12000,
    totalDisc: 12,
    totalPay: 12000,
    totalProductAct: 12,
    totalDiscTrxAct: 12,
    totalDiscAct: 12,
    totalPayAct: 12000,
    totalCollect: 12,
    totalPrint: 12,
    createdat: "20/20/2024",
    createdby: "admin",
    updatedat: "20/20/2024",
    updatedby: "admin",
    products: [
      {
        id: 1,
        code: "test",
        name: "test ID 1",
        price: 12000,
        qty: 12,
        qtyactual: 12000,
        disc1: 12000,
        discactual1: 12000,
        disc2: 12000,
        discactual2: 12000,
        disc3: 12000,
        discactual3: 12000,
        disc4: 12000,
        discactual4: 12000,
      },
      {
        id: 2,
        code: "test",
        name: "test ID 1",
        price: 12000,
        qty: 12,
        qtyactual: 12000,
        disc1: 12000,
        discactual1: 12000,
        disc2: 12000,
        discactual2: 12000,
        disc3: 12000,
        discactual3: 12000,
        disc4: 12000,
        discactual4: 12000,
      },
    ],
  },
  {
    id: 2,
    invoice: "INV12345",
    batch: "BATCH-1",
    batchDate: "20/20/2020",
    customer: "Toko Maju Jaya Abadi",
    invDate: "20/20/2020",
    deliveryDate: "20/20/2020",
    amount: 12000,
    actual: 12000,
    isactive: false,
    reason: "lorem ipsum",
    orderStatus: "NEW",
    totalProduct: 12,
    totalDiscTrx: 12000,
    totalDisc: 12,
    totalPay: 12000,
    totalProductAct: 12,
    totalDiscTrxAct: 12,
    totalDiscAct: 12,
    totalPayAct: 12000,
    totalCollect: 12,
    totalPrint: 12,
    createdat: "20/20/2024",
    createdby: "admin",
    updatedat: "20/20/2024",
    updatedby: "admin",
    products: [
      {
        id: 1,
        code: "test",
        name: "test ID 2",
        price: 12000,
        qty: 12,
        qtyactual: 12000,
        disc1: 12000,
        discactual1: 12000,
        disc2: 12000,
        discactual2: 12000,
        disc3: 12000,
        discactual3: 12000,
        disc4: 12000,
        discactual4: 12000,
      },
      {
        id: 2,
        code: "test",
        name: "test ID 3",
        price: 12000,
        qty: 12,
        qtyactual: 12000,
        disc1: 12000,
        discactual1: 12000,
        disc2: 12000,
        discactual2: 12000,
        disc3: 12000,
        discactual3: 12000,
        disc4: 12000,
        discactual4: 12000,
      },
    ],
  },
]);

// 👉 Headers
const headers = [
  { title: "", key: "data-table-expand" },
  { title: "Order No", key: "invoice" },
  { title: "Store Name", key: "customer" },
  { title: "Order date", key: "invDate" },
  { title: "Amount", key: "amount" },
  { title: "Actual", key: "actual" },
  { title: "Batch ID", key: "batch" },
  { title: "Batch Date", key: "batchDate" },
  { title: "Order Status", key: "orderStatus" },
];

const detailHeaders = [
  { title: "Product Code", key: "code" },
  { title: "Product Name", key: "name" },
  { title: "Qty", key: "qty" },
  { title: "Disc 1", key: "disc1" },
  { title: "Disc 2", key: "disc2" },
  { title: "Disc 3", key: "disc3" },
  { title: "Disc 4", key: "disc4" },
];

// Data table options
const itemsPerPage = ref(10);
const page = ref(1);
const sortBy = ref();
const orderBy = ref();
const selectedRows = ref([]);

// Update data table options

// 👉 search filters
const dateRange = ref("");
const dateRangeBatch = ref("");

const orderStatus = [
  { title: "NEW", value: "new" },
  { title: "ROUTED", value: "routed" },
  { title: "ON DELIVERY", value: "on delivery" },
  { title: "FULL DELIVERED", value: "full delivered" },
  { title: "PARTLY DELIVERED", value: "partly delivered" },
  { title: "NOT DELIVERED", value: "not delivered" },
  { title: "REJECTED", value: "rejected" },
  { title: "CANCELLED", value: "cancelled" },
];
</script>

<template>
  <section>
    <VCard class="mb-6">
      <VCardItem class="pb-4">
        <VCardTitle>Order</VCardTitle>
      </VCardItem>

      <!-- 👉 Filter -->
      <VCardText>
        <VRow>
          <!-- 👉 Select Date -->
          <VCol cols="12" sm="3">
            <AppDateTimePicker
              v-model="dateRange"
              placeholder="Order Date"
              clearable
              clear-icon="tabler-x"
              :config="{ mode: 'range' }"
              prepend-inner-icon="tabler-calendar"
            />
          </VCol>
          <!-- 👉 Select BatchDate -->
          <VCol cols="12" sm="3">
            <AppDateTimePicker
              v-model="dateRangeBatch"
              placeholder="Batch Date"
              clearable
              clear-icon="tabler-x"
              :config="{ mode: 'range' }"
              prepend-inner-icon="tabler-calendar"
            />
          </VCol>
          <!-- 👉 Select Order Status -->
          <VCol cols="12" sm="4">
            <AppSelect
              placeholder="Select Order Status"
              :items="orderStatus"
              clearable
              clear-icon="tabler-x"
            />
          </VCol>

          <!-- 👉 Apply Button -->
          <VCol cols="12" sm="2">
            <div class="d-flex align-items-center gap-2">
              <VBtn variant="outlined" color="info"> Apply </VBtn>
              <VBtn variant="text" color="error"> Reset </VBtn>
            </div>
          </VCol>
        </VRow>
      </VCardText>

      <VDivider />

      <VCardText class="d-flex flex-wrap gap-4">
        <div class="me-3 d-flex gap-3">
          <AppSelect
            :model-value="itemsPerPage"
            :items="[
              { value: 10, title: '10' },
              { value: 25, title: '25' },
              { value: 50, title: '50' },
              { value: 100, title: '100' },
              { value: -1, title: 'All' },
            ]"
            style="inline-size: 6.25rem"
            @update:model-value="itemsPerPage = parseInt($event, 10)"
          />
        </div>
        <VSpacer />

        <div class="app-user-search-filter d-flex align-center flex-wrap gap-4">
          <!-- 👉 Search  -->
          <div style="inline-size: 15.625rem">
            <AppTextField placeholder="Search Order" />
          </div>
          <VBtn
            color="primary"
            prepend-icon="tabler-file-upload"
            @click="isAddEditOrderDialogVisible = true"
          >
            Upload Order
          </VBtn>
        </div>
      </VCardText>

      <VDivider />

      <VDataTable
        :items="items"
        key="items.id"
        v-model:items-per-page="itemsPerPage"
        v-model:model-value="selectedRows"
        v-model:page="page"
        item-value="id"
        :headers="headers"
        class="text-no-wrap"
        expand-on-click
      >
        <!-- 👉 Expand -->
        <template #expanded-row="slotProps">
          <tr class="v-data-table__tr">
            <td :colspan="3" style="vertical-align: top">
              <p class="my-1">
                <span class="font-weight-bold">Total Products :</span>
                {{ slotProps.item.totalProduct }}
              </p>
              <p class="my-1">
                <span class="font-weight-bold"
                  >Total Discount Transaction :</span
                >
                {{ slotProps.item.totalDiscTrx }}
              </p>
              <p class="my-1">
                <span class="font-weight-bold">Total Discount :</span>
                {{ slotProps.item.totalDisc }}
              </p>
              <p class="my-1">
                <span class="font-weight-bold">Total Payment :</span>
                {{ slotProps.item.totalPay }}
              </p>
            </td>
            <td :colspan="3" style="vertical-align: top">
              <p class="my-1">
                <span class="font-weight-bold">Total Products Actual :</span>
                {{ slotProps.item.totalProductAct }}
              </p>
              <p class="my-1">
                <span class="font-weight-bold"
                  >Total Discount Transaction Actual :</span
                >
                {{ slotProps.item.totalDiscTrxAct }}
              </p>
              <p class="my-1">
                <span class="font-weight-bold">Total Discount Actual :</span>
                {{ slotProps.item.totalDiscAct }}
              </p>
              <p class="my-1">
                <span class="font-weight-bold">Total Payment Actual :</span>
                {{ slotProps.item.totalPayAct }}
              </p>
            </td>
            <td :colspan="3" style="vertical-align: top">
              <p class="my-1">
                <span class="font-weight-bold">Total Collection :</span>
                {{ slotProps.item.totalCollect }}
              </p>
              <p class="my-1">
                <span class="font-weight-bold">Total Print :</span>
                {{ slotProps.item.totalPrint }}
              </p>
              <p class="my-1">
                <span class="font-weight-bold">Reason :</span>
                {{ slotProps.item.reason }}
              </p>
            </td>
          </tr>
        </template>

        <!-- 👉 Invoice Link -->
        <template #item.invoice="{ item }">
          <div
            class="font-weight-bold text-primary text-decoration-underline"
            @click="isDetailOrderDialogVisible = true"
          >
            {{ item.invoice }}

            <VTooltip location="top" activator="parent"> View Detail </VTooltip>
          </div>
          <!-- 👉 Detail Invoice -->
          <VDialog
            :model-value="isDetailOrderDialogVisible"
            :width="$vuetify.display.smAndDown ? 'auto' : 1140"
          >
            <DialogCloseBtn @click="isDetailOrderDialogVisible = false" />

            <VCard class="pa-2 pa-sm-10">
              <VCardText>
                <!-- 👉 Title -->
                <h4 class="text-h4 text-center mb-6">{{ item.invoice }}</h4>
                <!-- Detail -->
                <VRow>
                  <VCol cols="12" sm="4">
                    <p class="my-1">
                      <span class="font-weight-bold">Total Products :</span>
                      {{ item.totalProduct }}
                    </p>
                    <p class="my-1">
                      <span class="font-weight-bold"
                        >Total Discount Transaction :</span
                      >
                      {{ item.totalDiscTrx }}
                    </p>
                    <p class="my-1">
                      <span class="font-weight-bold">Total Discount :</span>
                      {{ item.totalDisc }}
                    </p>
                    <p class="my-1">
                      <span class="font-weight-bold">Total Payment :</span>
                      {{ item.totalPay }}
                    </p>
                  </VCol>
                  <VCol cols="12" sm="4">
                    <p class="my-1">
                      <span class="font-weight-bold"
                        >Total Products Actual :</span
                      >
                      {{ item.totalProductAct }}
                    </p>
                    <p class="my-1">
                      <span class="font-weight-bold"
                        >Total Discount Transaction Actual :</span
                      >
                      {{ item.totalDiscTrxAct }}
                    </p>
                    <p class="my-1">
                      <span class="font-weight-bold"
                        >Total Discount Actual :</span
                      >
                      {{ item.totalDiscAct }}
                    </p>
                    <p class="my-1">
                      <span class="font-weight-bold"
                        >Total Payment Actual :</span
                      >
                      {{ item.totalPayAct }}
                    </p>
                  </VCol>
                  <VCol cols="12" sm="4">
                    <p class="my-1">
                      <span class="font-weight-bold">Total Collection :</span>
                      {{ item.totalCollect }}
                    </p>
                    <p class="my-1">
                      <span class="font-weight-bold">Total Print :</span>
                      {{ item.totalPrint }}
                    </p>
                    <p class="my-1">
                      <span class="font-weight-bold">Reason :</span>
                      {{ item.reason }}
                    </p>
                  </VCol>
                </VRow>
                <!-- 👉 List Product -->
                <VCard class="mb-6 mt-6">
                  <VCardItem class="pb-4">
                    <VCardTitle>List Product</VCardTitle>
                  </VCardItem>

                  <VDivider />

                  <VCardText class="d-flex flex-wrap gap-4">
                    <div class="me-3 d-flex gap-3">
                      <AppSelect
                        :model-value="itemsPerPage"
                        :items="[
                          { value: 10, title: '10' },
                          { value: 25, title: '25' },
                          { value: 50, title: '50' },
                          { value: 100, title: '100' },
                          { value: -1, title: 'All' },
                        ]"
                        style="inline-size: 6.25rem"
                        @update:model-value="
                          itemsPerPage = parseInt($event, 10)
                        "
                      />
                    </div>
                    <VSpacer />

                    <div
                      class="app-user-search-filter d-flex align-center flex-wrap gap-4"
                    >
                      <!-- 👉 Search  -->
                      <div style="inline-size: 15.625rem">
                        <AppTextField placeholder="Search Order" />
                      </div>
                    </div>
                  </VCardText>

                  <VDivider />

                  <VDataTable
                    :items="item.products"
                    v-model:items-per-page="itemsPerPage"
                    v-model:model-value="selectedRows"
                    v-model:page="page"
                    item-value="id"
                    :headers="detailHeaders"
                    class="text-no-wrap"
                  >
                    <template #item.qty="{ item }">
                      <div class="text-info">{{ item.qty }}</div>
                      <div class="text-muted text-sm-body-2">
                        Actual : {{ item.qtyactual }}
                      </div>
                    </template>
                    <!-- 👉 Disc -->
                    <template #item.disc1="{ item }">
                      <div class="text-info">{{ item.disc1 }}</div>
                      <div class="text-muted text-sm-body-2">
                        Actual : {{ item.discactual1 }}
                      </div>
                    </template>
                    <template #item.disc2="{ item }">
                      <div class="text-info">{{ item.disc2 }}</div>
                      <div class="text-muted text-sm-body-2">
                        Actual : {{ item.discactual2 }}
                      </div>
                    </template>
                    <template #item.disc3="{ item }">
                      <div class="text-info">{{ item.disc3 }}</div>
                      <div class="text-muted text-sm-body-2">
                        Actual : {{ item.discactual3 }}
                      </div>
                    </template>
                    <template #item.disc4="{ item }">
                      <div class="text-info">{{ item.disc4 }}</div>
                      <div class="text-muted text-sm-body-2">
                        Actual : {{ item.discactual4 }}
                      </div>
                    </template>
                  </VDataTable>
                </VCard>
              </VCardText>
            </VCard>
          </VDialog>
        </template>

        <!-- 👉 Order Status -->
        <template #item.orderStatus="{ item }">
          <div class="font-weight-bold">• {{ item.orderStatus }}</div>
        </template>
      </VDataTable>
    </VCard>

    <AddEditOrderDialog v-model:isDialogVisible="isAddEditOrderDialogVisible" />
  </section>
</template>
