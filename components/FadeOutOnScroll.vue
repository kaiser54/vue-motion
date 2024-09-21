<!-- components/FadeOutOnScroll.vue -->
<template>
  <div class="min-h-screen flex flex-col items-center justify-center">
    <div
      ref="textElement"
      v-motion
      :initial="{ opacity: 1 }"
      :enter="{ opacity: 1 }"
      :variants="{ fadeOut: { opacity: 0 } }"
      :style="{ opacity }"
      class="text-4xl font-bold text-center transition-opacity duration-300 ease-in-out"
    >
      Fade Out on Scroll
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { useMotion } from '@vueuse/motion'

const textElement = ref(null)
const opacity = ref(1)

const handleScroll = () => {
  const scrollPosition = window.scrollY
  const windowHeight = window.innerHeight
  const fadeStart = windowHeight * 0.2 // Start fading when 20% of the screen is scrolled
  const fadeEnd = windowHeight * 0.8 // Fully faded when 80% of the screen is scrolled
  const fadeRange = fadeEnd - fadeStart

  if (scrollPosition <= fadeStart) {
    opacity.value = 1
  } else if (scrollPosition >= fadeEnd) {
    opacity.value = 0
  } else {
    opacity.value = 1 - (scrollPosition - fadeStart) / fadeRange
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

const motion = useMotion(textElement)
</script>