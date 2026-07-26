<template>
  <div class="page home-page h-full flex flex-col">
    <!-- Header -->
    <div class="sticky top-0 z-10 bg-background">
      <div class="max-w-3xl mx-auto p-5 pb-3">
        <div class="flex justify-between items-center text-on-surface">
          <h1 class="text-xl font-semibold">Encore-Fork</h1>
        </div>
      </div>
    </div>

    <!-- Scrollable Content -->
    <div class="scrollbar-hidden pb-safe-nav flex-1 min-h-0 overflow-y-scroll">
      <div class="max-w-3xl mx-auto p-5 py-1">
        <!-- Daemon Status -->
        <div
          class="bg-secondary-container mb-4 p-4 rounded-xl flex items-center justify-between text-on-secondary-container"
        >
          <img
            :src="homeStore.logoImage"
            class="mx-2 w-20 h-20 object-contain shrink-0"
            alt="Encore Logo"
            rel="preload"
            tabindex="0"
          />
          <div class="flex-1 flex flex-col px-3 min-w-0">
            <span class="text-lg font-semibold truncate">{{ daemonStatusText }}</span>
            <span class="text-xs pt-1 block opacity-90 truncate">{{ daemonPidText }}</span>
          </div>
        </div>

        <!-- System Specifications & Module Info -->
        <div class="bg-surface-container mb-4 p-4 rounded-xl text-on-surface">
          <h2 class="text-xs font-bold uppercase tracking-wider text-on-surface-variant mb-3 px-1">
            System Specifications
          </h2>

          <div class="space-y-3.5">
            <!-- Device Model -->
            <div class="flex items-center justify-between gap-3">
              <div class="flex items-center gap-3 min-w-0">
                <AndroidIcon class="text-primary shrink-0 w-5 h-5" />
                <h3 class="text-sm font-medium text-on-surface truncate">
                  Device Model
                </h3>
              </div>
              <span class="allow-copy text-xs text-on-surface-variant font-medium shrink-0">{{
                displayValue(homeStore.deviceModel)
              }}</span>
            </div>

            <!-- Module Version -->
            <div class="flex items-center justify-between gap-3">
              <div class="flex items-center gap-3 min-w-0">
                <StarIcon class="text-primary shrink-0 w-5 h-5" />
                <h3 class="text-sm font-medium text-on-surface truncate">
                  {{ $t('home_page.info_card.module') }}
                </h3>
              </div>
              <span class="allow-copy text-xs text-on-surface-variant font-medium shrink-0">{{
                displayValue(homeStore.moduleVersion)
              }}</span>
            </div>

            <!-- Profile -->
            <div class="flex items-center justify-between gap-3">
              <div class="flex items-center gap-3 min-w-0">
                <StarlyGear class="text-primary shrink-0 w-5 h-5" />
                <h3 class="text-sm font-medium text-on-surface truncate">
                  {{ $t('home_page.info_card.profile') }}
                </h3>
              </div>
              <span class="allow-copy text-xs text-on-surface-variant font-medium shrink-0">{{
                currentProfileText
              }}</span>
            </div>

            <!-- CPU Governor -->
            <div class="flex items-center justify-between gap-3">
              <div class="flex items-center gap-3 min-w-0">
                <TuneIcon class="text-primary shrink-0 w-5 h-5" />
                <h3 class="text-sm font-medium text-on-surface truncate">
                  CPU Governor
                </h3>
              </div>
              <span class="allow-copy text-xs text-on-surface-variant font-medium shrink-0">{{
                displayValue(homeStore.cpuGovernor)
              }}</span>
            </div>

            <!-- System Memory -->
            <div class="flex items-center justify-between gap-3">
              <div class="flex items-center gap-3 min-w-0">
                <CandyIcon class="text-primary shrink-0 w-5 h-5" />
                <h3 class="text-sm font-medium text-on-surface truncate">
                  Memory (RAM)
                </h3>
              </div>
              <span class="allow-copy text-xs text-on-surface-variant font-medium shrink-0">{{
                displayValue(homeStore.memoryInfo)
              }}</span>
            </div>

            <!-- Chipset -->
            <div class="flex items-center justify-between gap-3">
              <div class="flex items-center gap-3 min-w-0">
                <ChipsetIcon class="text-primary shrink-0 w-5 h-5" />
                <h3 class="text-sm font-medium text-on-surface truncate">
                  {{ $t('home_page.info_card.chipset') }}
                </h3>
              </div>
              <span class="allow-copy text-xs text-on-surface-variant font-medium shrink-0">{{
                displayValue(homeStore.chipsetName)
              }}</span>
            </div>

            <!-- Kernel -->
            <div class="flex items-center justify-between gap-3">
              <div class="flex items-center gap-3 min-w-0">
                <ConsoleIcon class="text-primary shrink-0 w-5 h-5" />
                <h3 class="text-sm font-medium text-on-surface truncate">
                  {{ $t('home_page.info_card.kernel') }}
                </h3>
              </div>
              <span class="allow-copy text-xs text-on-surface-variant font-medium truncate max-w-[180px]">{{
                displayValue(homeStore.kernelVersion)
              }}</span>
            </div>

            <!-- Android Version & SDK -->
            <div class="flex items-center justify-between gap-3">
              <div class="flex items-center gap-3 min-w-0">
                <AndroidIcon class="text-primary shrink-0 w-5 h-5" />
                <h3 class="text-sm font-medium text-on-surface truncate">
                  Android & SDK
                </h3>
              </div>
              <span class="allow-copy text-xs text-on-surface-variant font-medium shrink-0">
                {{ displayValue(homeStore.androidVersion) }} (API {{ displayValue(homeStore.androidSDK) }})
              </span>
            </div>

            <!-- SELinux Status -->
            <div class="flex items-center justify-between gap-3">
              <div class="flex items-center gap-3 min-w-0">
                <CheckCircleIcon class="text-primary shrink-0 w-5 h-5" />
                <h3 class="text-sm font-medium text-on-surface truncate">
                  SELinux Status
                </h3>
              </div>
              <span class="allow-copy text-xs text-on-surface-variant font-medium shrink-0">{{
                displayValue(homeStore.selinuxMode)
              }}</span>
            </div>
          </div>
        </div>

        <!-- Live Daemon Log Monitor Card -->
        <div class="bg-surface-container mb-4 p-4 rounded-xl text-on-surface">
          <div class="flex items-center justify-between mb-3 px-1">
            <div class="flex items-center gap-2.5">
              <ConsoleIcon class="text-primary w-5 h-5 shrink-0" />
              <h2 class="text-sm font-semibold text-on-surface">Live Daemon Log</h2>
            </div>
            <button
              @click="fetchDaemonLogs"
              class="p-1.5 rounded-full hover:bg-surface-container-high transition-colors text-on-surface-variant"
              title="Refresh Log"
            >
              <RefreshIcon class="w-4 h-4 shrink-0" />
            </button>
          </div>
          <div
            ref="logContainer"
            class="bg-surface-container-high/60 p-3 rounded-lg font-mono text-xs text-on-surface-variant overflow-y-auto max-h-64 leading-relaxed select-text whitespace-pre-wrap word-break-all"
          >
            {{ daemonLogs || 'Loading daemon logs...' }}
          </div>
        </div>

        <!-- Fork Credit Badge -->
        <div class="mt-6 mb-3 text-center text-xs text-on-surface-variant flex items-center justify-center gap-1.5 opacity-80">
          <span>Encore-Fork</span>
          <span>&bull;</span>
          <span>Forked & Enhanced by</span>
          <a
            href="https://github.com/itswill00"
            target="_blank"
            class="font-semibold text-primary hover:underline"
          >@itswill00</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted, computed, ref, nextTick } from 'vue'
import { useHomeStore } from '@/stores/Home'
import * as KernelSU from '@/helpers/KernelSU'
import { useI18n } from 'vue-i18n'

import StarIcon from '@/components/icons/Star.vue'
import StarlyGear from '@/components/icons/StarlyGear.vue'
import ConsoleIcon from '@/components/icons/Console.vue'
import ChipsetIcon from '@/components/icons/Chipset.vue'
import AndroidIcon from '@/components/icons/Android.vue'
import RefreshIcon from '@/components/icons/Refresh.vue'
import TuneIcon from '@/components/icons/Tune.vue'
import CandyIcon from '@/components/icons/Candy.vue'
import CheckCircleIcon from '@/components/icons/CheckCircle.vue'

const { t } = useI18n()
const homeStore = useHomeStore()

const daemonLogs = ref('')
const logContainer = ref(null)
let logTimer = null

function displayValue(value) {
  if (value === 'unknown' || !value) {
    return t('common.unknown')
  }
  return value
}

const daemonStatusText = computed(() => {
  const status = homeStore.daemonStatusRaw
  if (status === 'loading') return t('common.loading')
  return t(`home_page.status_card.${status}`)
})

const daemonPidText = computed(() => {
  const status = homeStore.daemonStatusRaw
  if (status === 'running' && homeStore.daemonPidRaw) {
    return t('home_page.status_card.daemonPID', { pid: homeStore.daemonPidRaw })
  } else if (status === 'stopped') {
    return t('home_page.status_card.daemon_inactive')
  } else if (status === 'error' && homeStore.daemonError) {
    return homeStore.daemonError
  }
  return t('home_page.status_card.loading_daemon')
})

const currentProfileText = computed(() => {
  const profileKey = homeStore.currentProfileRaw
  if (profileKey === 'unknown' || !profileKey) return t('common.unknown')
  const translation = t(`profiles.${profileKey}`)
  return translation !== `profiles.${profileKey}` ? translation : profileKey
})

async function fetchDaemonLogs() {
  try {
    const logs = await KernelSU.readFile('/data/adb/.config/encore/encore.log')
    if (logs) {
      const lines = logs.split('\n')
      daemonLogs.value = lines.slice(-60).join('\n')
    } else {
      daemonLogs.value = 'No logs available.'
    }
  } catch (e) {
    daemonLogs.value = 'Waiting for log entries...'
  }
  await nextTick()
  if (logContainer.value) {
    logContainer.value.scrollTop = logContainer.value.scrollHeight
  }
}

onMounted(async () => {
  await homeStore.initializeData()
  await fetchDaemonLogs()
  logTimer = setInterval(fetchDaemonLogs, 3000)
})

onUnmounted(() => {
  if (logTimer) clearInterval(logTimer)
  homeStore.stopProfileMonitoring()
  homeStore.stopDaemonMonitoring()
})
</script>
