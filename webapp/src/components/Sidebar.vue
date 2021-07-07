<script lang="ts">
import { defineComponent, ref, onMounted, onUnmounted, PropType } from 'vue'
import { useRouter } from 'vue-router'
import { SidebarItem } from '~/types'
import IconDashboard from './IconDashboard.vue'
import IconTeam from './IconTeam.vue'
import IconTasks from './IconTasks.vue'
import IconApplications from './IconApplications.vue'
import IconSettings from './IconSettings.vue'
import { useEventListener } from '@vueuse/core'
import { useI18n } from 'vue-i18n'

export default defineComponent({
  name: 'Sidebar',
  props: {
    sidebarOpen: {
      type: Boolean,
      default: false,
    },
    items: {
      type: Array as PropType<SidebarItem[]>,
      default: () => ([
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
        { name: 'projects', icon: IconTasks, value: '/projects' },
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
      ]),
    },
  },
  emits: ['close-sidebar'],
  setup(props, { emit }) {
    const trigger = ref(null)
    const sidebar = ref(null)

    const currentRoute = useRouter().currentRoute.value
    const expandKeys = ref<string[]>([])
    const { t } = useI18n()

    function toggleExpandKey(key: SidebarItem['value']) {
      const idx = expandKeys.value.indexOf(key)
      if (idx < 0) expandKeys.value.push(key)
      else expandKeys.value.splice(idx, 1)
    }

    // close on click outside
    const clickHandler = ({ target }) => {
      if (!sidebar.value || !trigger.value) return
      if (
        !props.sidebarOpen
        || sidebar.value.contains(target)
        || trigger.value.contains(target)
      )
        return
      emit('close-sidebar')
    }

    // close if the esc key is pressed
    const keyHandler = ({ keyCode }: KeyboardEvent) => {
      if (!props.sidebarOpen || keyCode !== 27) return
      emit('close-sidebar')
    }

    useEventListener(document, 'click', clickHandler)
    useEventListener(document, 'keydown', keyHandler)

    return {
      t,
      trigger,
      sidebar,
      currentRoute,
      expandKeys,
      toggleExpandKey,
    }
  },
})
</script>
<template>
  <div class="lg:w-64">
    <!-- Sidebar backdrop (mobile only) -->
    <div
      class="fixed inset-0 bg-gray-900 bg-opacity-30 z-40 lg:hidden lg:z-auto transition-opacity duration-200"
      :class="sidebarOpen ? 'opacity-100' : 'opacity-0 pointer-events-none'"
      aria-hidden="true"
    ></div>

    <!-- Sidebar -->
    <div
      id="sidebar"
      ref="sidebar"
      class="absolute z-40 left-0 top-0 lg:static lg:left-auto lg:top-auto lg:translate-x-0 transform h-screen overflow-y-scroll lg:overflow-y-auto no-scrollbar w-64 flex-shrink-0 bg-gray-800 p-4 transition-transform duration-200 ease-in-out"
      :class="sidebarOpen ? 'translate-x-0' : '-translate-x-64'"
    >
      <!-- Sidebar header -->
      <div class="flex justify-between mb-10 pr-3 sm:px-2">
        <!-- Close button -->
        <button
          ref="trigger"
          class="lg:hidden text-gray-500 hover:text-gray-400"
          aria-controls="sidebar"
          :aria-expanded="sidebarOpen"
          @click.stop="$emit('close-sidebar')"
        >
          <span class="sr-only">Close sidebar</span>
          <svg class="w-6 h-6 fill-current" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path d="M10.7 18.7l1.4-1.4L7.8 13H20v-2H7.8l4.3-4.3-1.4-1.4L4 12z" />
          </svg>
        </button>
        <!-- Logo -->
        <router-link class="flex flex-1 items-center" to="/">
          <h1 class="text-xl mx-2 font-bold flex-1 text-center lg:order-1">STEEL ERP</h1>
          <svg width="32" height="32" viewBox="0 0 32 32">
            <defs>
              <linearGradient x1="28.538%" y1="20.229%" x2="100%" y2="108.156%" id="logo-a">
                <stop stop-color="#A5B4FC" stop-opacity="0" offset="0%" />
                <stop stop-color="#A5B4FC" offset="100%" />
              </linearGradient>
              <linearGradient x1="88.638%" y1="29.267%" x2="22.42%" y2="100%" id="logo-b">
                <stop stop-color="#38BDF8" stop-opacity="0" offset="0%" />
                <stop stop-color="#38BDF8" offset="100%" />
              </linearGradient>
            </defs>
            <rect fill="#6366F1" width="32" height="32" rx="16" />
            <path
              d="M18.277.16C26.035 1.267 32 7.938 32 16c0 8.837-7.163 16-16 16a15.937 15.937 0 01-10.426-3.863L18.277.161z"
              fill="#4F46E5"
            />
            <path
              d="M7.404 2.503l18.339 26.19A15.93 15.93 0 0116 32C7.163 32 0 24.837 0 16 0 10.327 2.952 5.344 7.404 2.503z"
              fill="url(#logo-a)"
            />
            <path
              d="M2.223 24.14L29.777 7.86A15.926 15.926 0 0132 16c0 8.837-7.163 16-16 16-5.864 0-10.991-3.154-13.777-7.86z"
              fill="url(#logo-b)"
            />
          </svg>
        </router-link>
      </div>

      <!-- Links -->
      <div>
        <h3 class="text-xs uppercase text-gray-500 font-semibold pl-3">Pages</h3>
        <ul class="mt-3">
          <li
            v-for="item in items"
            :key="item.name"
            class="px-3 py-2 rounded-sm mb-0.5 last:mb-0 text-gray-200 hover:text-white hover:bg-gray-900 transition"
            :class="currentRoute.path.startsWith(item.value) ? 'bg-gray-900' : ''"
          >
            <router-link
              :to="item.children ? '' : item.value"
              @click="item.children && toggleExpandKey(item.value)"
            >
              <div class="flex flex-grow items-center">
                <!-- 动态图标 -->
                <component
                  :is="item.icon"
                  class="flex-shrink-0 h-6 w-6 mr-3"
                  :active="currentRoute.path.startsWith(item.value)"
                />
                <span class="text-sm font-medium flex-1">{{ t(`menus.${item.name}`) }}</span>
                <akar-icons-chevron-up
                  v-if="item.children && expandKeys.includes(item.value)"
                  class="text-sm mr-1"
                />
                <akar-icons-chevron-down
                  v-if="item.children && !expandKeys.includes(item.value)"
                  class="text-sm mr-1"
                />
                <span
                  v-if="item.tips && item.tips > 0"
                  class="inline-flex items-center justify-center h-5 text-xs font-medium text-white bg-indigo-500 px-2 rounded-sm"
                >{{ item.tips }}</span>
              </div>
            </router-link>
            <ul v-if="item.children && expandKeys.includes(item.value)" class="pl-9 mt-1">
              <li
                v-for="sub in item.children"
                :key="sub.value"
                class="py-1 block hover:text-indigo-400 text-gray-200 transition"
                :class="currentRoute.path.startsWith(sub.value) ? 'text-indigo-400' : 'text-gray-200'"
              >
                <router-link :to="sub.value" class="block text-sm">{{ t(`menus.${sub.name}`) }}</router-link>
              </li>
            </ul>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
