<script setup lang="ts">
//👉 - Dummy Interface Data
interface Items {
  id: number;
  storeCode: string;
  customer: string;
}

//👉 - Dummy Object Data
const items = ref<Items[]>([
  {
    id: 1,
    storeCode: "123123123",
    customer: "TOKO RIZKY GANG BAHAGIA NO 25",
  },
  {
    id: 1,
    storeCode: "123123123",
    customer: "TOKO RIZKY GANG BAHAGIA NO 25",
  },

]);

// 👉 Headers
const headers = [
  { title: "Code", key: "storeCode" },
  { title: "Customer", key: "customer" },
];

// Data table options
const itemsPerPage = ref(10);
const page = ref(1);
const sortBy = ref();
const orderBy = ref();
const selectedRows = ref([]);

const props = defineProps<Props>();
const emit = defineEmits<Emit>();

interface Props {
  isDialogVisible: boolean;
}

interface Emit {
  (e: "update:isDialogVisible", val: boolean): void;
}

const dialogVisibleUpdate = (val: boolean) => {
  emit("update:isDialogVisible", val);
};
</script>

<template>
  <VDialog :model-value="props.isDialogVisible" :width="$vuetify.display.smAndDown ? 'auto' : 1140"
    @update:model-value="dialogVisibleUpdate">
    <DialogCloseBtn @click="emit('update:isDialogVisible', false)" />

    <VCard class="pa-2 pa-sm-10">
      <VCardText>
        <!-- 👉 Title -->
        <h4 class="text-h4 text-center mb-6">Missing Order</h4>

        <!-- 👉 Result Upload -->
        <VCard class="mb-6 mt-6">
          <VDataTable :items="items" key="items.id" v-model:items-per-page="itemsPerPage"
            v-model:model-value="selectedRows" v-model:page="page" item-value="id" :headers="headers"
            class="text-no-wrap">
          </VDataTable>
        </VCard>

      </VCardText>
    </VCard>
  </VDialog>
</template>

<style lang="scss">
.refer-link-input {
  .v-field--appended {
    padding-inline-end: 0;
  }

  .v-field__append-inner {
    padding-block-start: 0.125rem;
  }
}
</style>
