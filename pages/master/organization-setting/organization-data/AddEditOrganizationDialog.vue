<script setup lang="ts">
const props = defineProps<Props>();
const emit = defineEmits<Emit>();

const timeOpen = ref("");
const timeClose = ref("");
const startTime = ref("");
const endTime = ref("");
const vehicleSchedule = ref(false)

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
  <VDialog
    :model-value="props.isDialogVisible"
    :width="$vuetify.display.smAndDown ? 'auto' : 900"
    @update:model-value="dialogVisibleUpdate"
  >
    <DialogCloseBtn @click="emit('update:isDialogVisible', false)" />

    <VCard class="pa-2 pa-sm-10">
      <VCardText>
        <!-- 👉 Title -->
        <h4 class="text-h4 text-center mb-6">Add Organization</h4>

        <!-- 👉 Form -->
        <VForm class="mt-6">
          <VRow>
            <!-- 👉 Company Name -->
            <VCol cols="12" md="6">
              <AppTextField label="Company Name" placeholder="Company Name" />
            </VCol>

            <!-- 👉 Parent -->
            <VCol cols="12" md="6">
              <AppSelect
                :items="['Foo', 'Bar', 'Fizz', 'Buzz']"
                label="Parent"
                placeholder="Parent"
              />
            </VCol>

            <!-- 👉 Longitude -->
            <VCol cols="12" md="3">
              <AppTextField label="Longitude" placeholder="Longitude" />
            </VCol>

            <!-- 👉 Latitude -->
            <VCol cols="12" md="3">
              <AppTextField label="Latitude" placeholder="Latitude" />
            </VCol>

            <!-- 👉 Open -->
            <VCol cols="12" md="3">
              <AppDateTimePicker
                v-model="timeOpen"
                label="Open Hour"
                placeholder="Open Hour"
                :config="{
                  enableTime: true,
                  noCalendar: true,
                  dateFormat: 'H:i',
                }"
              />
            </VCol>

            <!-- 👉 Close -->
            <VCol cols="12" md="3">
              <AppDateTimePicker
                v-model="timeClose"
                label="Close Hour"
                placeholder="Close Hour"
                :config="{
                  enableTime: true,
                  noCalendar: true,
                  dateFormat: 'H:i',
                }"
              />
            </VCol>

            <!-- 👉 Address -->
            <VCol cols="12">
              <AppTextField label="Address" placeholder="Address" />
            </VCol>

            <VCol cols="12">
              <VCard class="mb-6 mt-6">
                <VCardItem class="pb-4">
                  <VSwitch v-model="vehicleSchedule" density="compact" label="Vehicle Schedule?" />
                </VCardItem>

                <VDivider />

                <v-table v-if="vehicleSchedule">
                  <thead>
                    <tr>
                      <th class="text-left">Day</th>
                      <th class="text-left">Start Time</th>
                      <th class="text-left">End Time</th>
                      <th class="text-left">Duration</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr>
                      <td>Senin</td>
                      <td>
                        <AppDateTimePicker
                          v-model="startTime"
                          placeholder="Select time"
                          :config="{
                            enableTime: true,
                            noCalendar: true,
                            dateFormat: 'H:i',
                          }"
                        />
                      </td>
                      <td>
                        <AppDateTimePicker
                          v-model="endTime"
                          placeholder="Select time"
                          :config="{
                            enableTime: true,
                            noCalendar: true,
                            dateFormat: 'H:i',
                          }"
                        />
                      </td>
                      <td>
                        <AppTextField  placeholder="Duration" />
                      </td>
                    </tr>
                    <tr>
                      <td>Selasa</td>
                      <td>
                        <AppDateTimePicker
                          v-model="startTime"
                          placeholder="Select time"
                          :config="{
                            enableTime: true,
                            noCalendar: true,
                            dateFormat: 'H:i',
                          }"
                        />
                      </td>
                      <td>
                        <AppDateTimePicker
                          v-model="endTime"
                          placeholder="Select time"
                          :config="{
                            enableTime: true,
                            noCalendar: true,
                            dateFormat: 'H:i',
                          }"
                        />
                      </td>
                      <td>
                        <AppTextField  placeholder="Duration" />
                      </td>
                    </tr>
                  </tbody>
                </v-table>
              </VCard>
            </VCol>

            <!-- 👉 Switch Status -->
            <VCol cols="12">
              <VSwitch density="compact" label="Is Active?" />
            </VCol>

            <!-- 👉 Submit and Cancel -->
            <VCol cols="12" class="d-flex flex-wrap justify-center gap-4">
              <VBtn type="submit"> Add Data </VBtn>

              <VBtn color="secondary" variant="tonal"> Cancel </VBtn>
            </VCol>
          </VRow>
        </VForm>
      </VCardText>
    </VCard>
  </VDialog>
</template>

<style></style>
