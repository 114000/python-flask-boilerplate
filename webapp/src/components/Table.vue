<script lang="ts">
import { defineComponent } from 'vue'
import { useI18n } from 'vue-i18n'

export default defineComponent({
  props: {
    title: {
      type: String,
      default: '',
    },
    items: {
      type: Array,
      default: () => ([]),
    },
    columns: {
      type: Array,
      default: () => ([]),
    },
    total: {
      type: Number,
      default: 0,
    },
    pageCount: {
      type: Number,
      default: 10,
    },
    page: {
      type: Number,
      default: 1,
    },
    checkable: {
      type: Boolean,
      default: false,
    },
  },
  setup() {
    const { t } = useI18n()

    return {
      t,
    }
  },
})
</script>
<template>
  <div class="bg-white shadow-lg rounded-sm border border-gray-200 relative">
    <header class="px-5 py-4">
      <h2 class="font-semibold text-gray-800">
        {{ t('table.all') }} {{ title }}
        <span class="text-gray-400 font-medium">442</span>
      </h2>
    </header>
    <div>
      <!-- Table -->
      <div class="overflow-x-auto">
        <table class="table-auto w-full">
          <!-- Table header -->
          <thead
            class="text-xs font-semibold uppercase text-gray-500 bg-gray-50 border-t border-b border-gray-200"
          >
            <tr>
              <th v-if="checkable" class="px-2 first:pl-5 last:pr-5 py-3 whitespace-nowrap w-px">
                <div class="flex items-center">
                  <label class="inline-flex">
                    <span class="sr-only">Select all</span>
                    <input class="form-checkbox" type="checkbox" />
                  </label>
                </div>
              </th>
              <th
                v-for="(col, i) in columns"
                :key="i"
                class="px-2 first:pl-5 last:pr-5 py-3 whitespace-nowrap"
              >
                <div class="font-semibold text-left">{{ t(col.label) }}</div>
              </th>
            </tr>
          </thead>
          <tbody class="text-sm"></tbody>
          <!-- Table body -->
          <tr
            v-for="(item, i) in items"
            :key="i"
          >
            <td
              v-for="(col, j) in columns"
              :key="j"
              class="px-2 first:pl-5 last:pr-5 py-3 whitespace-nowrap">
              <div class="flex items-center text-gray-800">
                <!-- <div
                  class="w-10 h-10 flex-shrink-0 flex items-center justify-center bg-gray-100 rounded-full mr-2 sm:mr-3"
                >
                  <img class="ml-1" :src="order.image" width="20" height="20" :alt="order.order" />
                </div> -->
                <div class="font-medium">{{ item[col.prop] }}</div>
              </div>
            </td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>
