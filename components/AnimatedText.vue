<!-- components/AnimatedText.vue -->
<template>
  <div class="animated-text">
    <span
      v-for="(letter, index) in text"
      :key="index"
      v-motion
      :initial="{ opacity: 0, y: 50 }"
      :enter="{ 
        opacity: 1, 
        y: 0, 
        transition: { 
          type: 'spring', 
          stiffness: 250, 
          damping: 25, 
          delay: index * 50 
        } 
      }"
    >
      {{ letter }}
    </span>
  </div>
</template>

<script setup>
const text = "Value-driven Innovations for Food Enterprises".split('')
console.log(text)
</script>

<style scoped>
.animated-text {
  font-size: 2rem;
  font-weight: bold;
  display: flex;
  justify-content: center;
}

span {
  display: inline-block;
  margin-right: 2px;
}
</style>