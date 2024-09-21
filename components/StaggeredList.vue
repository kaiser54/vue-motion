<!-- components/StaggeredList.vue -->
<template>
  <div>
    <h2>Staggered Animation Example</h2>
    <ul>
      <li
        v-for="(item, index) in items"
        :key="item"
        v-motion
        :initial="{ opacity: 0, y: 100 }"
        :enter="{ opacity: 1, y: 0, transition: { delay: index * 100 } }"
      >
        {{ item }}
      </li>
    </ul>
  </div>
</template>

<script setup>
const items = [
  'Item 1',
  'Item 2',
  'Item 3',
  'Item 4',
  'Item 5',
]
</script>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
  font-size: 18px;
}
</style>