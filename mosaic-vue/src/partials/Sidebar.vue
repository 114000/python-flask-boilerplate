<template>
  <div class="lg:w-64">
    <!-- Sidebar backdrop (mobile only) -->
    <div class="fixed inset-0 bg-gray-900 bg-opacity-30 z-40 lg:hidden lg:z-auto transition-opacity duration-200" :class="sidebarOpen ? 'opacity-100' : 'opacity-0 pointer-events-none'" aria-hidden="true"></div>

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
          @click.stop="$emit('close-sidebar')"
          aria-controls="sidebar"
          :aria-expanded="sidebarOpen"
        >
          <span class="sr-only">Close sidebar</span>
          <svg class="w-6 h-6 fill-current" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path d="M10.7 18.7l1.4-1.4L7.8 13H20v-2H7.8l4.3-4.3-1.4-1.4L4 12z" />
          </svg>
        </button>
        <!-- Logo -->
        <router-link class="block" to="/">
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
            <path d="M18.277.16C26.035 1.267 32 7.938 32 16c0 8.837-7.163 16-16 16a15.937 15.937 0 01-10.426-3.863L18.277.161z" fill="#4F46E5" />
            <path d="M7.404 2.503l18.339 26.19A15.93 15.93 0 0116 32C7.163 32 0 24.837 0 16 0 10.327 2.952 5.344 7.404 2.503z" fill="url(#logo-a)" />
            <path d="M2.223 24.14L29.777 7.86A15.926 15.926 0 0132 16c0 8.837-7.163 16-16 16-5.864 0-10.991-3.154-13.777-7.86z" fill="url(#logo-b)" />
          </svg>
        </router-link>
      </div>

      <!-- Links -->
      <div>
        <h3 class="text-xs uppercase text-gray-500 font-semibold pl-3">Pages</h3>
        <ul class="mt-3">
          <!-- Dashboard -->
          <router-link to="/" custom v-slot="{ href, navigate, isExactActive }">
            <li class="px-3 py-2 rounded-sm mb-0.5 last:mb-0" :class="isExactActive && 'bg-gray-900'">
              <a class="block text-gray-200 hover:text-white transition duration-150" :class="isExactActive && 'hover:text-gray-200'" :href="href" @click="navigate">
                <div class="flex flex-grow">
                  <svg class="flex-shrink-0 h-6 w-6 mr-3" viewBox="0 0 24 24">
                    <path class="fill-current text-gray-400" :class="isExactActive && 'text-indigo-500'" d="M12 0C5.383 0 0 5.383 0 12s5.383 12 12 12 12-5.383 12-12S18.617 0 12 0z" />
                    <path class="fill-current text-gray-600" :class="isExactActive && 'text-indigo-600'" d="M12 3c-4.963 0-9 4.037-9 9s4.037 9 9 9 9-4.037 9-9-4.037-9-9-9z" />
                    <path class="fill-current text-gray-400" :class="isExactActive && 'text-indigo-200'" d="M12 15c-1.654 0-3-1.346-3-3 0-.462.113-.894.3-1.285L6 6l4.714 3.301A2.973 2.973 0 0112 9c1.654 0 3 1.346 3 3s-1.346 3-3 3z" />
                  </svg>
                  <span class="text-sm font-medium">Dashboard</span>
                </div>
              </a>
            </li>
          </router-link>
          <!-- Customers -->
          <router-link to="/customers" custom v-slot="{ href, navigate, isExactActive }">
            <li class="px-3 py-2 rounded-sm mb-0.5 last:mb-0" :class="isExactActive && 'bg-gray-900'">
              <a class="block text-gray-200 hover:text-white transition duration-150" :class="isExactActive && 'hover:text-gray-200'" :href="href" @click="navigate">
                <div class="flex flex-grow">
                  <svg class="flex-shrink-0 h-6 w-6 mr-3" viewBox="0 0 24 24">
                    <path class="fill-current text-gray-400" :class="isExactActive && 'text-indigo-300'" d="M7 0l6 7H8v10H6V7H1z" />
                    <path class="fill-current text-gray-600" :class="isExactActive && 'text-indigo-500'" d="M18 7v10h5l-6 7-6-7h5V7z" />
                  </svg>
                  <span class="text-sm font-medium">Customers</span>
                </div>
              </a>
            </li>
          </router-link>
          <!-- Orders -->
          <router-link to="/orders" custom v-slot="{ href, navigate, isExactActive }">
            <li class="px-3 py-2 rounded-sm mb-0.5 last:mb-0" :class="isExactActive && 'bg-gray-900'">
              <a class="block text-gray-200 hover:text-white transition duration-150" :class="isExactActive && 'hover:text-gray-200'" :href="href" @click="navigate">
                <div class="flex items-center justify-between">
                  <div class="flex flex-grow">
                    <svg class="flex-shrink-0 h-6 w-6 mr-3" viewBox="0 0 24 24">
                      <path class="fill-current text-gray-400" :class="isExactActive && 'text-indigo-300'" d="M13 15l11-7L11.504.136a1 1 0 00-1.019.007L0 7l13 8z" />
                      <path class="fill-current text-gray-700" :class="isExactActive && 'text-indigo-600'" d="M13 15L0 7v9c0 .355.189.685.496.864L13 24v-9z" />
                      <path class="fill-current text-gray-600" :class="isExactActive && 'text-indigo-500'" d="M13 15.047V24l10.573-7.181A.999.999 0 0024 16V8l-11 7.047z" />
                    </svg>
                    <span class="text-sm font-medium">Orders</span>
                  </div>
                  <!-- Badge -->
                  <div class="flex flex-shrink-0 ml-2">
                    <span class="inline-flex items-center justify-center h-5 text-xs font-medium text-white bg-indigo-500 px-2 rounded-sm">4</span>
                  </div>
                </div>
              </a>
            </li>
          </router-link>
          <!-- Campaigns -->
          <router-link to="/campaigns" custom v-slot="{ href, navigate, isExactActive }">
            <li class="px-3 py-2 rounded-sm mb-0.5 last:mb-0" :class="isExactActive && 'bg-gray-900'">
              <a class="block text-gray-200 hover:text-white transition duration-150" :class="isExactActive && 'hover:text-gray-200'" :href="href" @click="navigate">
                <div class="flex flex-grow">
                  <svg class="flex-shrink-0 h-6 w-6 mr-3" viewBox="0 0 24 24">
                    <path class="fill-current text-gray-600" :class="isExactActive && 'text-indigo-500'" d="M20 7a.75.75 0 01-.75-.75 1.5 1.5 0 00-1.5-1.5.75.75 0 110-1.5 1.5 1.5 0 001.5-1.5.75.75 0 111.5 0 1.5 1.5 0 001.5 1.5.75.75 0 110 1.5 1.5 1.5 0 00-1.5 1.5A.75.75 0 0120 7zM4 23a.75.75 0 01-.75-.75 1.5 1.5 0 00-1.5-1.5.75.75 0 110-1.5 1.5 1.5 0 001.5-1.5.75.75 0 111.5 0 1.5 1.5 0 001.5 1.5.75.75 0 110 1.5 1.5 1.5 0 00-1.5 1.5A.75.75 0 014 23z" />
                    <path class="fill-current text-gray-400" :class="isExactActive && 'text-indigo-300'" d="M17 23a1 1 0 01-1-1 4 4 0 00-4-4 1 1 0 010-2 4 4 0 004-4 1 1 0 012 0 4 4 0 004 4 1 1 0 010 2 4 4 0 00-4 4 1 1 0 01-1 1zM7 13a1 1 0 01-1-1 4 4 0 00-4-4 1 1 0 110-2 4 4 0 004-4 1 1 0 112 0 4 4 0 004 4 1 1 0 010 2 4 4 0 00-4 4 1 1 0 01-1 1z" />
                  </svg>
                  <span class="text-sm font-medium">Campaigns</span>
                </div>
              </a>
            </li>
          </router-link>
          <!-- Team -->
          <router-link to="/team-tabs" custom v-slot="{ href, navigate }">
            <li class="px-3 py-2 rounded-sm mb-0.5 last:mb-0" :class="currentRoute.fullPath.includes('team-') && 'bg-gray-900'">
              <a class="block text-gray-200 hover:text-white transition duration-150" :class="currentRoute.fullPath.includes('team-') && 'hover:text-gray-200'" :href="href" @click="navigate">
                <div class="flex items-center justify-between">
                  <div class="flex flex-grow">
                    <svg class="flex-shrink-0 h-6 w-6 mr-3" viewBox="0 0 24 24">
                      <path class="fill-current text-gray-600" :class="currentRoute.fullPath.includes('team-') && 'text-indigo-500'" d="M18.974 8H22a2 2 0 012 2v6h-2v5a1 1 0 01-1 1h-2a1 1 0 01-1-1v-5h-2v-6a2 2 0 012-2h.974zM20 7a2 2 0 11-.001-3.999A2 2 0 0120 7zM2.974 8H6a2 2 0 012 2v6H6v5a1 1 0 01-1 1H3a1 1 0 01-1-1v-5H0v-6a2 2 0 012-2h.974zM4 7a2 2 0 11-.001-3.999A2 2 0 014 7z" />
                      <path class="fill-current text-gray-400" :class="currentRoute.fullPath.includes('team-') && 'text-indigo-300'" d="M12 6a3 3 0 110-6 3 3 0 010 6zm2 18h-4a1 1 0 01-1-1v-6H6v-6a3 3 0 013-3h6a3 3 0 013 3v6h-3v6a1 1 0 01-1 1z" />
                    </svg>
                    <span class="text-sm font-medium">Team</span>
                  </div>
                  <!-- Icon -->
                  <div class="flex flex-shrink-0 ml-2">
                    <svg class="w-3 h-3 flex-shrink-0 ml-1 fill-current text-gray-400" :class="currentRoute.fullPath.includes('team-') && 'transform rotate-180'" viewBox="0 0 12 12">
                      <path d="M5.9 11.4L.5 6l1.4-1.4 4 4 4-4L11.3 6z" />
                    </svg>
                  </div>
                </div>
              </a>
              <ul class="pl-9 mt-1" :class="!currentRoute.fullPath.includes('team-') && 'hidden'">
                <router-link to="/team-tabs" custom v-slot="{ href, navigate, isExactActive }">
                  <li class="mb-1 last:mb-0">
                    <a class="block text-gray-200 hover:text-white transition duration-150" :class="isExactActive && 'text-indigo-400 hover:text-indigo-400'" :href="href" @click="navigate">
                      <span class="text-sm font-medium">Team - Tabs</span>
                    </a>
                  </li>
                </router-link>
                <router-link to="/team-tiles" custom v-slot="{ href, navigate, isExactActive }">
                  <li class="mb-1 last:mb-0">
                    <a class="block text-gray-200 hover:text-white transition duration-150" :class="isExactActive && 'text-indigo-400 hover:text-indigo-400'" :href="href" @click="navigate">
                      <span class="text-sm font-medium">Team - Tiles</span>
                    </a>
                  </li>
                </router-link>                
              </ul>
            </li>
          </router-link>          
          <!-- Messages -->
          <router-link to="/messages" custom v-slot="{ href, navigate, isExactActive }">
            <li class="px-3 py-2 rounded-sm mb-0.5 last:mb-0" :class="isExactActive && 'bg-gray-900'">
              <a class="block text-gray-200 hover:text-white transition duration-150" :class="isExactActive && 'hover:text-gray-200'" :href="href" @click="navigate">
                <div class="flex flex-grow">
                  <svg class="flex-shrink-0 h-6 w-6 mr-3" viewBox="0 0 24 24">
                    <path class="fill-current text-gray-600" :class="isExactActive && 'text-indigo-500'" d="M14.5 7c4.695 0 8.5 3.184 8.5 7.111 0 1.597-.638 3.067-1.7 4.253V23l-4.108-2.148a10 10 0 01-2.692.37c-4.695 0-8.5-3.184-8.5-7.11C6 10.183 9.805 7 14.5 7z" />
                    <path class="fill-current text-gray-400" :class="isExactActive && 'text-indigo-300'" d="M11 1C5.477 1 1 4.582 1 9c0 1.797.75 3.45 2 4.785V19l4.833-2.416C8.829 16.85 9.892 17 11 17c5.523 0 10-3.582 10-8s-4.477-8-10-8z" />
                  </svg>
                  <span class="text-sm font-medium">Messages</span>
                </div>
              </a>
            </li>
          </router-link>
          <!-- Tasks -->
          <router-link to="/tasks" custom v-slot="{ href, navigate, isExactActive }">
            <li class="px-3 py-2 rounded-sm mb-0.5 last:mb-0" :class="isExactActive && 'bg-gray-900'">
              <a class="block text-gray-200 hover:text-white transition duration-150" :class="isExactActive && 'hover:text-gray-200'" :href="href" @click="navigate">
                <div class="flex flex-grow">
                  <svg class="flex-shrink-0 h-6 w-6 mr-3" viewBox="0 0 24 24">
                    <path class="fill-current text-gray-600" :class="isExactActive && 'text-indigo-500'" d="M8 1v2H3v19h18V3h-5V1h7v23H1V1z" />
                    <path class="fill-current text-gray-600" :class="isExactActive && 'text-indigo-500'" d="M1 1h22v23H1z" />
                    <path class="fill-current text-gray-400" :class="isExactActive && 'text-indigo-300'" d="M15 10.586L16.414 12 11 17.414 7.586 14 9 12.586l2 2zM5 0h14v4H5z" />
                  </svg>
                  <span class="text-sm font-medium">Tasks</span>
                </div>
              </a>
            </li>
          </router-link>
          <!-- Applications -->
          <router-link to="/applications" custom v-slot="{ href, navigate, isExactActive }">
            <li class="px-3 py-2 rounded-sm mb-0.5 last:mb-0" :class="isExactActive && 'bg-gray-900'">
              <a class="block text-gray-200 hover:text-white transition duration-150" :class="isExactActive && 'hover:text-gray-200'" :href="href" @click="navigate">
                <div class="flex flex-grow">
                  <svg class="flex-shrink-0 h-6 w-6 mr-3" viewBox="0 0 24 24">
                    <circle class="fill-current text-gray-400" :class="isExactActive && 'text-indigo-300'" cx="18.5" cy="5.5" r="4.5" />
                    <circle class="fill-current text-gray-600" :class="isExactActive && 'text-indigo-500'" cx="5.5" cy="5.5" r="4.5" />
                    <circle class="fill-current text-gray-600" :class="isExactActive && 'text-indigo-500'" cx="18.5" cy="18.5" r="4.5" />
                    <circle class="fill-current text-gray-400" :class="isExactActive && 'text-indigo-300'" cx="5.5" cy="18.5" r="4.5" />
                  </svg>
                  <span class="text-sm font-medium">Applications</span>
                </div>
              </a>
            </li>
          </router-link>
          <!-- Settings -->
          <router-link to="/settings" custom v-slot="{ href, navigate, isExactActive }">
            <li class="px-3 py-2 rounded-sm mb-0.5 last:mb-0" :class="isExactActive && 'bg-gray-900'">
              <a class="block text-gray-200 hover:text-white transition duration-150" :class="isExactActive && 'hover:text-gray-200'" :href="href" @click="navigate">
                <div class="flex flex-grow">
                  <svg class="flex-shrink-0 h-6 w-6 mr-3" viewBox="0 0 24 24">
                    <path class="fill-current text-gray-600" :class="isExactActive && 'text-indigo-500'" d="M19.714 14.7l-7.007 7.007-1.414-1.414 7.007-7.007c-.195-.4-.298-.84-.3-1.286a3 3 0 113 3 2.969 2.969 0 01-1.286-.3z" />
                    <path class="fill-current text-gray-400" :class="isExactActive && 'text-indigo-300'" d="M10.714 18.3c.4-.195.84-.298 1.286-.3a3 3 0 11-3 3c.002-.446.105-.885.3-1.286l-6.007-6.007 1.414-1.414 6.007 6.007z" />
                    <path class="fill-current text-gray-600" :class="isExactActive && 'text-indigo-500'" d="M5.7 10.714c.195.4.298.84.3 1.286a3 3 0 11-3-3c.446.002.885.105 1.286.3l7.007-7.007 1.414 1.414L5.7 10.714z" />
                    <path class="fill-current text-gray-400" :class="isExactActive && 'text-indigo-300'" d="M19.707 9.292a3.012 3.012 0 00-1.415 1.415L13.286 5.7c-.4.195-.84.298-1.286.3a3 3 0 113-3 2.969 2.969 0 01-.3 1.286l5.007 5.006z" />
                  </svg>
                  <span class="text-sm font-medium">Settings</span>
                </div>
              </a>
            </li>
          </router-link>
        </ul>
      </div>

    </div>
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue'
import { useRouter } from 'vue-router'

export default {
  name: 'Sidebar',
  props: ['sidebarOpen'],
  setup(props, { emit }) {
    const trigger = ref(null)
    const sidebar = ref(null)

    const currentRoute = useRouter().currentRoute.value

    // close on click outside
    const clickHandler = ({ target }) => {
      if (!sidebar.value || !trigger.value) return
      if (
        !props.sidebarOpen ||
        sidebar.value.contains(target) ||
        trigger.value.contains(target)
      )
        return
      emit('close-sidebar')
    }

    // close if the esc key is pressed
    const keyHandler = ({ keyCode }) => {
      if (!props.sidebarOpen || keyCode !== 27) return
      emit('close-sidebar')
    }

    onMounted(() => {
      document.addEventListener('click', clickHandler)
      document.addEventListener('keydown', keyHandler)
    })

    onUnmounted(() => {
      document.removeEventListener('click', clickHandler)
      document.removeEventListener('keydown', keyHandler)
    })

    return {
      trigger,
      sidebar,
      currentRoute,
    }
  },
}
</script>