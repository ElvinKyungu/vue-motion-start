<script setup lang="ts">
import { initialTabs as tabs } from './gradient'
import { AnimatePresence, Motion } from 'motion-v'

const selectedTab = ref(tabs[0])
</script>

<template>
  <div class="flex flex-col justify-center items-center w-full min-h-screen bg-black ">
    <div class="h-screen w-full"></div>
    <div class="w-[480px] h-[360px] max-w-[320px] rounded-[10px] bg-gray-800 overflow-hidden shadow-[0_1px_1px_rgba(0,0,0,0.075),0_2px_2px_rgba(0,0,0,0.075),0_4px_4px_rgba(0,0,0,0.075),0_8px_8px_rgba(0,0,0,0.075),0_16px_16px_rgba(0,0,0,0.075)] flex flex-col">
      <nav class="bg-muted p-[5px_5px_0] rounded-[10px] h-11">
        <ul class="flex w-full">
          <li
            v-for="item in tabs"
            :key="item.label"
            :class="{ 'bg-primary': item === selectedTab }"
            class="rounded-[5px] rounded-b-none  text-white w-full p-[10px_15px]   cursor-pointer h-6 flex justify-between items-center flex-1 min-w-0 relative select-none  font-medium text-sm"
            @click="selectedTab = item"
          >
            {{ item.icon }} {{ item.label }}
            <Motion
              v-if="item.label === selectedTab.label"
              class="absolute bottom-[-10px] left-0 right-0 h-[1px] bg-red-500"
              layout-id="underline"
            />
          </li>
        </ul>
      </nav>
      <main class="flex justify-center items-center text-[128px] flex-grow select-none">
        <AnimatePresence mode="wait">
          <Motion
            :key="selectedTab ? selectedTab.label : 'empty'"
            :initial="{ y: 10, opacity: 0 }"
            :animate="{ y: 0, opacity: 1 }"
            :exit="{ y: -10, opacity: 0 }"
            :transition="{ duration: 0.2 }"
          >
            {{ selectedTab ? selectedTab.icon : '😋' }}
          </Motion>
        </AnimatePresence>
      </main>
    </div>
    <div class="flex justify-center gap-4">
      <Motion
        as="div"
        :animate="{ 
          scale:[1,1.2,2, 1],
          rotate: [0, 90, 180, 360],
          borderRadius: ['0%', '50%', '50%', '50%'],
        }"
        :transition="{
          duration: 2,
          ease: 'easeInOut',
          times: [0, 0.2, 0.5, 0.8, 1],
          repeat: Infinity,
          repeatDelay: 1,
        }"
        class="w-20 h-20  bg-white my-20 shadow-[0_1px_1px_rgba(0,0,0,0.075),0_2px_2px_rgba(0,0,0,0.075),0_4px_4px_rgba(0,0,0,0.075),0_8px_8px_rgba(0,0,0,0.075),0_16px_16px_rgba(0,0,0,0.075)]"
      />
    </div>
  </div>
</template>

