<script setup lang="ts">
const peopleOptions = computed(() =>
  [
    {
      value: 'add',
      label: 'Adding Groups',
      icon: 'i-ep:circle-plus',
    },
  ],
)

const peopleSelected = ref('')
const isOpen = ref(false)
const groupName = ref('')
const loading = ref(false)

function handleGroupsChange(val: string) {
  // eslint-disable-next-line no-console
  console.log('groups changed', val)

  if (val === 'add') {
    isOpen.value = true
  }
}

function handleSumbit() { }

watch(() => peopleSelected.value, (val) => {
  // eslint-disable-next-line no-console
  console.log("🚀 ~ watch ~ val:", val)
})
</script>

<template>
  <div>
    <USelectMenu v-model="peopleSelected" class="w-[9rem]" :clear-search-on-close="true" searchable
      :options="peopleOptions" placeholder="please Select groups" value-attribute="value" option-attribute="label"
      @change="handleGroupsChange" />

    <UModal v-model="isOpen" prevent-close>
      <UCard :ui="{ ring: '', divide: 'divide-y divide-gray-100 dark:divide-gray-800' }">
        <template #header>
          <div class="flex items-center justify-between">
            <h3 class="text-base font-semibold leading-6 text-gray-900 dark:text-white">
              shortLink.addGroup
            </h3>
            <UButton color="gray" variant="ghost" icon="i-heroicons-x-mark-20-solid" class="-my-1"
              @click="isOpen = false" />
          </div>
        </template>

        <UFormGroup label="shortLink.groupName" required>
          <UInput v-model="groupName" name="groupName" placeholder="shortLink.pleaseEnterGroupName" autocomplete="off"
            :ui="{ icon: { trailing: { pointer: '' } } }">
            <template #trailing>
              <UButton v-show="groupName !== ''" color="gray" variant="link" icon="i-heroicons-x-mark-20-solid"
                :padded="false" @click="groupName = ''" />
            </template>
          </UInput>
        </UFormGroup>

        <template #footer>
          <div class="flex items-center justify-end gap-2">
            <UButton color="white" label="cancel" @click="isOpen = false" />
            <UButton label="confirm" :loading="loading" @click="handleSumbit" />
          </div>
        </template>
      </UCard>
    </UModal>
  </div>
</template>
