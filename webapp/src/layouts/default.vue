<script lang="ts">
import { defineComponent, ref } from 'vue'
import { IconDashboard, IconTeam, IconTasks, IconApplications, IconSettings } from '~/partials/sidebar'

export default defineComponent({
  setup() {
    const sidebarOpen = ref(false)
    const items = [
      { name: 'dashboard', icon: IconDashboard, value: '/dashboard' },
      {
        name: 'permission',
        icon: IconTeam,
        value: '/permission',
        children: [
          { name: 'permission', value: '/permission/permissions' },
          { name: 'roles', value: '/permission/roles' },
          { name: 'users', value: '/permission/users' },
        ],
      },
      {
        name: 'projects',
        icon: IconTasks,
        value: '/projects',
        children: [
          { name: 'daily', value: '/projects/daily' },
        ],
      },
      {
        name: 'monitor',
        value: '/monitor',
        icon: IconApplications,
        children: [
          { name: 'cameras', value: '/monitor/cameras' },
          { name: 'screens', value: '/monitor/screens' },
        ],
      },
      { name: 'settings', value: '/settings', icon: IconSettings, tips: 6 },
    ]
    return {
      sidebarOpen,
      items,
    }
  },
})
</script>
<template>
  <NMessageProvider>
    <div class="flex h-screen overflow-hidden">
      <Sidebar
        :items="items"
        :sidebar-open="sidebarOpen"
        @close-sidebar="sidebarOpen = false"
      />
      <div class="main">
        <Header
          :sidebar-open="sidebarOpen"
          @toggle-sidebar="sidebarOpen = !sidebarOpen"
        />
        <main>
          <div class="content">
            <router-view></router-view>
          </div>
        </main>
        <div class="footer-brand">Copyright Steel ERP</div>
      </div>
    </div>
  </NMessageProvider>
</template>
<style scoped lang="postcss">
.main {
  @apply
    relative flex flex-col flex-1
    overflow-y-auto overflow-x-hidden
    bg-blue-gray-100;
}
.content {
  @apply px-4 sm:px-6 lg:px-8 py-8 w-full max-w-9xl mx-auto;
}

.footer-brand {
  @apply mt-5 mx-auto text-center opacity-25 text-sm;
}
</style>
