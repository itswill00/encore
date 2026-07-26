<template>
  <div class="page home-page h-full flex flex-col">
    <!-- Header -->
    <div class="sticky top-0 z-10 bg-background/80 backdrop-blur-md border-b border-surface-container-high/40">
      <div class="max-w-3xl mx-auto p-5 py-3.5 flex justify-between items-center text-on-surface">
        <div>
          <h1 class="text-xl font-bold tracking-tight">Encore-Fork</h1>
          <p class="text-xs text-on-surface-variant">tanzanite · MT6789</p>
        </div>
        <div class="flex items-center gap-2">
          <span
            class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-semibold"
            :class="homeStore.daemonStatusRaw === 'running' ? 'bg-primary/15 text-primary border border-primary/30' : 'bg-error/15 text-error border border-error/30'"
          >
            <span class="w-2 h-2 rounded-full" :class="homeStore.daemonStatusRaw === 'running' ? 'bg-primary animate-pulse' : 'bg-error'"></span>
            {{ daemonStatusText }}
          </span>
        </div>
      </div>
    </div>

    <!-- Scrollable Content -->
    <div class="scrollbar-hidden pb-safe-nav flex-1 min-h-0 overflow-y-scroll">
      <div class="max-w-3xl mx-auto p-5 py-3 space-y-4">
        <!-- Hero Daemon Status Card -->
        <div
          class="bg-surface-container p-5 rounded-2xl flex items-center justify-between text-on-surface border border-surface-container-high shadow-sm"
        >
          <div class="flex items-center gap-4">
            <div class="relative">
              <img
                :src="homeStore.logoImage"
                class="w-16 h-16 object-contain"
                alt="Encore Logo"
                rel="preload"
              />
            </div>
            <div class="flex flex-col">
              <span class="text-base font-bold text-on-surface">{{ daemonStatusText }}</span>
              <span class="text-xs text-on-surface-variant mt-0.5">{{ daemonPidText }}</span>
              <span class="text-xs font-medium text-primary mt-1">Profile: {{ currentProfileText }}</span>
            </div>
          </div>
        </div>

        <!-- Quick Profile Status Overview -->
        <div class="bg-surface-container p-4 rounded-2xl border border-surface-container-high text-on-surface">
          <h2 class="text-xs font-bold uppercase tracking-wider text-on-surface-variant mb-3">
            Active Performance Profile
          </h2>
          <div class="grid grid-cols-3 gap-2">
            <div
              class="p-3 rounded-xl border text-center transition-all cursor-default"
              :class="homeStore.currentProfileRaw === 'performance' ? 'bg-primary/15 border-primary text-primary font-bold shadow-sm' : 'bg-surface border-surface-container-high text-on-surface-variant opacity-70'"
            >
              <div class="text-lg mb-1">⚡</div>
              <div class="text-xs font-semibold">Performance</div>
            </div>
            <div
              class="p-3 rounded-xl border text-center transition-all cursor-default"
              :class="homeStore.currentProfileRaw === 'balance' || homeStore.currentProfileRaw === 'perfcommon' ? 'bg-primary/15 border-primary text-primary font-bold shadow-sm' : 'bg-surface border-surface-container-high text-on-surface-variant opacity-70'"
            >
              <div class="text-lg mb-1">⚖️</div>
              <div class="text-xs font-semibold">Balance</div>
            </div>
            <div
              class="p-3 rounded-xl border text-center transition-all cursor-default"
              :class="homeStore.currentProfileRaw === 'powersave' ? 'bg-primary/15 border-primary text-primary font-bold shadow-sm' : 'bg-surface border-surface-container-high text-on-surface-variant opacity-70'"
            >
              <div class="text-lg mb-1">🍃</div>
              <div class="text-xs font-semibold">Powersave</div>
            </div>
          </div>
        </div>

        <!-- Device & Module Info -->
        <div class="bg-surface-container p-4 rounded-2xl text-on-surface border border-surface-container-high">
          <h2 class="text-xs font-bold uppercase tracking-wider text-on-surface-variant mb-2 px-1">
            System Specifications
          </h2>
          
          <div class="divide-y divide-surface-container-high">
            <div class="py-2.5 px-2 flex items-center justify-between">
              <div class="flex items-center gap-3">
                <StarIcon class="text-primary w-4 h-4 shrink-0" />
                <span class="text-xs font-medium text-on-surface">{{ $t('home_page.info_card.module') }}</span>
              </div>
              <span class="allow-copy text-xs font-semibold text-on-surface-variant">{{ displayValue(homeStore.moduleVersion) }}</span>
            </div>

            <div class="py-2.5 px-2 flex items-center justify-between">
              <div class="flex items-center gap-3">
                <StarlyGear class="text-primary w-4 h-4 shrink-0" />
                <span class="text-xs font-medium text-on-surface">{{ $t('home_page.info_card.profile') }}</span>
              </div>
              <span class="allow-copy text-xs font-semibold text-on-surface-variant">{{ currentProfileText }}</span>
            </div>

            <div class="py-2.5 px-2 flex items-center justify-between">
              <div class="flex items-center gap-3">
                <ConsoleIcon class="text-primary w-4 h-4 shrink-0" />
                <span class="text-xs font-medium text-on-surface">{{ $t('home_page.info_card.kernel') }}</span>
              </div>
              <span class="allow-copy text-xs font-semibold text-on-surface-variant truncate max-w-[200px]">{{ displayValue(homeStore.kernelVersion) }}</span>
            </div>

            <div class="py-2.5 px-2 flex items-center justify-between">
              <div class="flex items-center gap-3">
                <ChipsetIcon class="text-primary w-4 h-4 shrink-0" />
                <span class="text-xs font-medium text-on-surface">{{ $t('home_page.info_card.chipset') }}</span>
              </div>
              <span class="allow-copy text-xs font-semibold text-on-surface-variant">{{ displayValue(homeStore.chipsetName) }}</span>
            </div>

            <div class="py-2.5 px-2 flex items-center justify-between">
              <div class="flex items-center gap-3">
                <AndroidIcon class="text-primary w-4 h-4 shrink-0" />
                <span class="text-xs font-medium text-on-surface">{{ $t('home_page.info_card.androidSDK') }}</span>
              </div>
              <span class="allow-copy text-xs font-semibold text-on-surface-variant">{{ displayValue(homeStore.androidSDK) }}</span>
            </div>
          </div>
        </div>

        <!-- Device Specific Enhancements (Tanzanite) -->
        <div
          v-if="homeStore.isTanzaniteDevice"
          class="bg-surface-container p-4 rounded-2xl text-on-surface border border-primary/30"
        >
          <div class="flex items-center gap-3 mb-2.5">
            <div class="w-8 h-8 rounded-xl bg-primary/15 flex items-center justify-center shrink-0">
              <StarIcon class="text-primary w-4 h-4" />
            </div>
            <div>
              <h3 class="text-sm font-bold text-primary">Tanzanite Special Enhancements</h3>
              <span class="text-xs text-on-surface-variant">Redmi Note 14 4G (MT6789)</span>
            </div>
          </div>
          <div class="text-xs text-on-surface-variant space-y-2 pt-1">
            <div class="flex items-center gap-2 bg-surface/50 p-2 rounded-lg">
              <span class="w-2 h-2 rounded-full bg-primary shrink-0"></span>
              <span>GED GPU Floor 800MHz (Gaming) / 550MHz (UI)</span>
            </div>
            <div class="flex items-center gap-2 bg-surface/50 p-2 rounded-lg">
              <span class="w-2 h-2 rounded-full bg-primary shrink-0"></span>
              <span>sugov_ext Rate Limits & Touch Idle Bypass</span>
            </div>
            <div class="flex items-center gap-2 bg-surface/50 p-2 rounded-lg">
              <span class="w-2 h-2 rounded-full bg-primary shrink-0"></span>
              <span>PSI Memory Stall Auto-Trim Active</span>
            </div>
          </div>
        </div>

        <!-- Support Me Button -->
        <RippleComponent
          @click="handleDonateClick"
          tabindex="0"
          class="cursor-pointer text-on-surface bg-surface-container p-4 rounded-2xl w-full border border-surface-container-high block"
        >
          <h2 class="text-sm font-bold mb-1 relative z-10">
            {{ $t('home_page.support_button.title') }}
          </h2>
          <p class="text-xs text-on-surface-variant relative z-10">
            {{ $t('home_page.support_button.description') }}
          </p>
        </RippleComponent>

        <!-- Learn Encore -->
        <RippleComponent
          @click="handleGuideClick"
          tabindex="0"
          class="cursor-pointer text-on-surface bg-surface-container p-4 rounded-2xl w-full border border-surface-container-high block"
        >
          <h2 class="text-sm font-bold mb-1 relative z-10">
            {{ $t('home_page.learn_encore.title') }}
          </h2>
          <p class="text-xs text-on-surface-variant relative z-10">
            {{ $t('home_page.learn_encore.description') }}
          </p>
        </RippleComponent>

        <!-- Fork Credit Badge -->
        <div class="pt-4 pb-2 text-center text-xs text-on-surface-variant flex items-center justify-center gap-1.5 opacity-80">
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
import { onMounted, onUnmounted, computed } from 'vue'
import { useHomeStore } from '@/stores/Home'
import * as KernelSU from '@/helpers/KernelSU'
import { useI18n } from 'vue-i18n'

import RippleComponent from '@/components/ui/Ripple.vue'
import StarIcon from '@/components/icons/Star.vue'
import StarlyGear from '@/components/icons/StarlyGear.vue'
import ConsoleIcon from '@/components/icons/Console.vue'
import ChipsetIcon from '@/components/icons/Chipset.vue'
import AndroidIcon from '@/components/icons/Android.vue'

const { t } = useI18n()
const homeStore = useHomeStore()

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

onMounted(async () => {
  await homeStore.initializeData()
})

onUnmounted(() => {
  homeStore.stopProfileMonitoring()
  homeStore.stopDaemonMonitoring()
})

function handleGuideClick() {
  KernelSU.openWebsite('https://encore.rem01gaming.dev')
}

function handleDonateClick() {
  KernelSU.openWebsite('https://t.me/rem01schannel/670')
}
</script>
