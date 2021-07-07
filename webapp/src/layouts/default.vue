<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
  setup() {
    const sidebarOpen = ref(false)

    return {
      sidebarOpen,
    }
  },
})
</script>
<template>
  <NMessageProvider>
    <div class="flex h-screen overflow-hidden">
      <Sidebar :sidebar-open="sidebarOpen" @close-sidebar="sidebarOpen = false" />
      <div class="relative flex flex-col flex-1 overflow-y-auto overflow-x-hidden">
        <Header :sidebar-open="sidebarOpen" @toggle-sidebar="sidebarOpen = !sidebarOpen" />
        <main>
          <div class="px-4 sm:px-6 lg:px-8 py-8 w-full max-w-9xl mx-auto">
            <router-view></router-view>
          </div>
        </main>
        <div class="mt-5 mx-auto text-center opacity-25 text-sm">[Default Layout]</div>
      </div>
    </div>
  </NMessageProvider>
</template>
