<script lang="ts">
import { useI18n } from 'vue-i18n'
import { computed, defineComponent, ref } from 'vue'
import { useRouter } from 'vue-router'
import { accessApi } from '~/api'
import { useUser } from '~/logic'
import { SigninPayload, SigninDto } from '~/types'
export default defineComponent({
  setup() {
    const router = useRouter()
    const { setUser } = useUser()
    const { t } = useI18n()
    const param = ref<SigninPayload>({
      name: 'David',
      pwd: '123456',
    })

    const disabled = computed(() => {
      return param.value.name === '' || param.value.pwd === ''
    })

    function signin(e: Event) {
      e.preventDefault()

      if (disabled.value) return

      accessApi.signin(param.value)
        .then((dto: SigninDto) => {
          setUser(dto)
          router.push('/dashboard')
        })
    }

    return {
      signin,
      param,
      disabled,
      t,
    }
  },
})
</script>
<template>
  <main class="bg-white">
    <div class="relative md:flex">
      <!-- Content -->
      <div class="md:w-1/2">
        <div class="max-w-sm mx-auto min-h-screen flex flex-col justify-center px-4 py-8">
          <div class="w-full">
            <h1 class="text-3xl text-gray-800 font-bold mb-6">
              {{ t('access.welcome_back') }} ✨
            </h1>
            <!-- Form -->
            <form @submit="signin">
              <div class="space-y-4">
                <div>
                  <label class="block text-sm font-medium mb-1" for="email">Email Address</label>
                  <input id="email" class="form-input w-full" />
                </div>
                <div>
                  <label class="block text-sm font-medium mb-1" for="password">Password</label>
                  <input id="password" class="form-input w-full" type="password" autocomplete="on" />
                </div>
              </div>
              <div class="flex items-center justify-between mt-6">
                <div class="mr-1">
                  <router-link
                    class="text-sm underline hover:no-underline"
                    to="/reset-password"
                  >Forgot Password?</router-link>
                </div>
                <button
                  type="submit"
                  class="btn bg-indigo-500 hover:bg-indigo-600 text-white ml-3"
                >{{ t('access.sign_in') }}</button>
              </div>
            </form>
            <!-- Footer -->
            <div class="pt-5 mt-6 border-t border-gray-200">
              <div class="text-sm">
                Don’t you have an account?
                <router-link
                  class="font-medium text-indigo-500 hover:text-indigo-600"
                  to="/signup"
                >Sign Up</router-link>
              </div>
              <!-- Warning -->
              <div class="mt-5">
                <div class="bg-yellow-100 text-yellow-600 px-3 py-2 rounded">
                  <svg class="inline w-3 h-3 flex-shrink-0 fill-current mr-2" viewBox="0 0 12 12">
                    <path
                      d="M10.28 1.28L3.989 7.575 1.695 5.28A1 1 0 00.28 6.695l3 3a1 1 0 001.414 0l7-7A1 1 0 0010.28 1.28z"
                    />
                  </svg>
                  <span
                    class="text-sm"
                  >To support you during the pandemic super pro features are free until March 31st.</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Image -->
      <div class="hidden md:block absolute top-0 bottom-0 right-0 md:w-1/2" aria-hidden="true">
        <img
          class="object-cover object-center w-full h-full"
          src="../../images/auth-image.jpg"
          width="760"
          height="1024"
          alt="Authentication"
        />
        <img
          class="absolute top-1/4 left-0 transform -translate-x-1/2 ml-8"
          src="../../images/auth-decoration.png"
          width="218"
          height="224"
          alt="Authentication decoration"
        />
      </div>
    </div>
  </main>
</template>
<route lang="yaml">
meta:
  layout: empty
</route>
