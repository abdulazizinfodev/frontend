<script>
import axios from 'axios'
import Toast from '@/components/Toast.vue'
import { useToastStore } from '@/stores/toast'
import { useUserStore } from '@/stores/user'
import { RouterLink } from 'vue-router'

export default {
    setup() {
        const userStore = useUserStore()
        const toastStore = useToastStore()

        return {
            userStore,
            toastStore
        }
    },

    components: {
        Toast,
        RouterLink
    },

    methods: {
        logout() {
            console.log('Log out')

            this.userStore.removeToken()

            this.$router.push('/login')
        },
    },
}
</script>

<template>
    <div class="relative transform overflow-hidden rounded-lg text-left transition-all sm:my-8 sm:w-full sm:max-w-lg">
        <div class="px-4 pb-4">
            <div class="hidden sm:flex sm:flex-1 sm:items-center sm:justify-start">
                <img class="w-20 h-20 rounded-full ms-2 transition duration-75" :src="userStore.user.avatar"
                    alt="user photo" />
                <div class="min-w-0 px-3">
                    <p class="text-sm font-semibold leading-6 text-gray-100">{{ userStore.user.name }}</p>
                    <p class="mt-1 truncate text-xs leading-5 text-gray-100">{{ userStore.user.username }}</p>
                </div>
            </div>
            <div class="items-start justify-start md:hidden">
                <div class="mx-auto h-20 w-20 flex-shrink-0 items-start justify-start rounded-full sm:mx-0 sm:h-10 sm:w-10">
                    <img class="w-20 h-20 rounded-full ms-2 transition duration-75" :src="userStore.user.avatar"
                        alt="user photo" />
                </div>
                <div class="mt-3 text-center sm:ml-4 sm:mt-0 sm:text-left">
                    <div class="min-w-0">
                        <p class="text-sm font-semibold leading-6 text-gray-100">{{ userStore.user.name }}</p>
                        <p class="mt-1 truncate text-xs leading-5 text-gray-100">{{ userStore.user.username }}</p>
                    </div>
                </div>
            </div>
        </div>
        <div class="justify-start p-4 space-x-4 lg:flex">
            <a @click="logout"
                class="flex items-center p-2 text-base text-gray-300 cursor-alias bg-gray-700 font-semibold rounded-full group">
                <svg class="ms-3 w-4 h-4 text-gray-300 transition duration-75" aria-hidden="true"
                    xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 16 16">
                    <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M4 8h11m0 0-4-4m4 4-4 4m-5 3H3a2 2 0 0 1-2-2V3a2 2 0 0 1 2-2h3" />
                </svg>
                <span class="flex-1 ml-1 mr-3 whitespace-nowrap">Logout</span>
            </a>
        </div>
    </div>
</template>