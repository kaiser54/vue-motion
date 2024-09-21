<!-- components/InteractiveItems.vue -->
<template>
  <div>
    <div v-for="item in items" :key="item.id">
      <div
        v-motion
        :layout-id="item.id"
        @click="setSelectedId(item.id)"
        class="cursor-pointer p-4 bg-gray-100 mb-2 rounded"
      >
        <h5 v-motion>{{ item.subtitle }}</h5>
        <h2 v-motion class="text-xl font-bold">{{ item.title }}</h2>
      </div>
    </div>

    <motion-presence>
      <motion
        v-if="selectedId"
        :layout-id="selectedId"
        :initial="{ opacity: 0, scale: 0.8 }"
        :enter="{ opacity: 1, scale: 1 }"
        :exit="{ opacity: 0, scale: 0.8 }"
        class="fixed top-0 left-0 w-full h-full flex items-center justify-center bg-black bg-opacity-50"
      >
        <div class="bg-white p-8 rounded-lg">
          <h5 v-motion>{{ selectedItem.subtitle }}</h5>
          <h2 v-motion class="text-2xl font-bold mb-4">{{ selectedItem.title }}</h2>
          <button
            v-motion
            @click="setSelectedId(null)"
            class="bg-blue-500 text-white px-4 py-2 rounded"
          >
            Close
          </button>
        </div>
      </motion>
    </motion-presence>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { Motion, MotionPresence } from '@vueuse/motion'

const items = [
  { id: 1, title: 'Item 1', subtitle: 'Subtitle 1' },
  { id: 2, title: 'Item 2', subtitle: 'Subtitle 2' },
  { id: 3, title: 'Item 3', subtitle: 'Subtitle 3' },
]

const selectedId = ref(null)

const setSelectedId = (id) => {
  selectedId.value = id
}

const selectedItem = computed(() => 
  items.find(item => item.id === selectedId.value) || {}
)
</script>