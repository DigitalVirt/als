<script setup>
import { darkTheme, useOsTheme, zhCN, dateZhCN } from 'naive-ui'
import { useAppStore } from './stores/app'
import LoadingCard from '@/components/Loading.vue'
import InfoCard from '@/components/Information.vue'
import SpeedtestCard from '@/components/Speedtest.vue'
import UtilitiesCard from '@/components/Utilities.vue'
import TrafficCard from '@/components/TrafficDisplay.vue'
import { computed } from 'vue'

const lang = computed(() => {
  return zhCN
})

const dateLang = computed(() => {
  return dateZhCN
})
const osThemeRef = useOsTheme()
const theme = computed(() => (osThemeRef.value === 'dark' ? darkTheme : null))
const appStore = useAppStore()
</script>

<template>
    <header class="w-full shadow-sm flex items-center">
        <div class="relative container w-full mx-auto sm:flex sm:items-center sm:justify-between" aria-label="Global">
            <a href="https://digitalvirt.com" class="brand">
                DigitalVirt
            </a>
            <nav class="ms-auto gap-x-3">
                <a href="https://digitalvirt.com" class="hover:text-blue-600">官方网站</a>
            </nav>
        </div>
    </header>
    <n-config-provider class="container w-full mx-auto py-6" :locale="lang" :date-locale="dateLang" :theme="theme">
    <n-global-style />
        <n-message-provider>
            <n-space vertical>
                <h2 class="text-xl mb-4">Looking Glass Server</h2>
                <LoadingCard v-if="appStore.connecting" />
                <template v-else>
                    <InfoCard />
                    <UtilitiesCard />
                    <SpeedtestCard />
                    <TrafficCard v-if="appStore.config.feature_iface_traffic" />
                </template>
                <div style="margin-top: 10px">
                    Powered by DigitalVirt                   
                </div>
                <div>Memory usage: {{ appStore.memoryUsage }}</div>
            </n-space>
        </n-message-provider>
    </n-config-provider>
</template>
