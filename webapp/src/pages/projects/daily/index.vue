
<script lang="ts">
import { ref } from 'vue'
import { useI18n } from 'vue-i18n'
import DeleteButton from '~/partials/actions/DeleteButton.vue'
import DateSelect from '~/partials/actions/DateSelect.vue'
import FilterButton from '~/partials/actions/FilterButton.vue'
import OrdersTable from '~/partials/orders/OrdersTable.vue'
import PaginationClassic from '~/partials/PaginationClassic.vue'
import PaginationNumeric from '~/partials/PaginationNumeric.vue'
import { jsonToExcel, downloadFile } from '~/utils/Utils'
export default {
  name: 'Orders',
  components: {
    DeleteButton,
    DateSelect,
    FilterButton,
    OrdersTable,
    PaginationClassic,
    PaginationNumeric,
  },
  setup() {
    const sidebarOpen = ref(false)
    const selectedItems = ref([])
    const { t } = useI18n()
    const columns = [
      { prop: 'item_name', label: 'business.item_name' },
      { prop: 'project_no', label: 'business.project_no' },
      { prop: 'work_address', label: 'business.work_address' },
      { prop: 'work_content', label: 'business.work_content' },
      { prop: 'safety_points', label: 'business.safety_points' },
      { prop: 'work_org', label: 'business.work_org' },
      { prop: 'work_leader', label: 'business.work_leader' },
      { prop: 'checker', label: 'business.checker' },
      { prop: 'equipment_leader', label: 'business.equipment_leader' },
    ]

    const items = [
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
      { item_name: 'Apple', project_no: '12', work_address: 'New York', work_content: 'Party', safety_points: 'None', work_org: 'China Mobile', work_leader: 'Xiaochuang Wang', checker: 'Banana', equipment_leader: 'Orange', remarks: 'Hi! This is a perfect ERP system.' },
    ]

    const updateSelectedItems = (selected) => {
      selectedItems.value = selected
    }

    const downloadExcel = () => {
      const excelHeads = columns.map(col => t(col.label))
      const excelContents = items.map(item => {
        return columns.map(col => item[col.prop])
      })
      
      excelContents.unshift(excelHeads)

      jsonToExcel(excelContents)
        .then(blob => {
         downloadFile(blob, '每日项目计划.xlsx')
        })
    }

    return {
      t,
      sidebarOpen,
      selectedItems,
      updateSelectedItems,
      downloadExcel,
      columns,
      items,
    }
  },
}
</script>
<template>
  <!-- Page header -->
  <PageHead :title="t('menus.daily') + ' ✨'">
    <Button @click="downloadExcel">
      <ic-baseline-download class="text-base" />
    </Button>
    <DeleteButton :selectedItems="selectedItems" />
    <!-- Filter button -->
    <FilterButton />
    <!-- Dropdown -->
    <DateSelect />
    <!-- Add customer button -->
    <router-link to="/projects/daily/0">
      <Button class="bg-indigo-500 hover:bg-indigo-600">
        <ant-design-plus-outlined class="text-white" />
        <span class="hidden xs:block ml-2">Add {{ t('business.construction') }}</span>
      </Button>
    </router-link>
  </PageHead>

  <Table
    :title="t('business.construction')"
    :columns="columns"
    :items="items"
  />

  <PaginationNumeric class="py-4" />

  <!-- Table -->
  <OrdersTable @change-selection="updateSelectedItems($event)" />

  <!-- Pagination -->
  <div class="mt-8">
    <PaginationClassic />
  </div>
</template>

