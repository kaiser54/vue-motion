<template>
  <div class="max-w-xl">
    <div ref="header">
      <h1 class="text-6xl">
        <span class="sr-only">Value-driven Innovations for Food Enterprises</span>
        <span
          v-for="(letter, index) in text"
          :key="index"
          v-motion
          v-if="inView"
          :initial="{ opacity: 0, y: 30, filter: 'blur(5px)' }"
          :enter="{
            opacity: 1,
            y: 0,
            filter: 'blur(0px)',
            transition: {
              type: 'spring',
              stiffness: 90,
              damping: 50,
              delay: index * 70,
            },
          }"
        >
          {{ letter }}
        </span>
      </h1>
      
      <p class="text-2xl">
        <span class="sr-only">Independent Purchasing Company Ltd (IPC) transforms restaurant and
          food service industry supply chains, making them more efficient and valuable
        </span>
        <span
          v-for="(word, index) in snippet"
          :key="index + word"
          v-motion
          v-if="inView"
          :initial="{ opacity: 0, y: 20, filter: 'blur(5px)' }"
          :enter="{
            opacity: 1,
            y: 0,
            filter: 'blur(0px)',
            transition: {
              type: 'spring',
              stiffness: 90,
              damping: 50,
              delay: (text.length + index) * 70,
            },
          }"
        >{{ word }}</span>
      </p>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

// Text data outside the setup function
const text = "Value-driven Innovations for Food Enterprises".split(" ");
const snippet =
  "Independent Purchasing Company Ltd (IPC) transforms restaurant and food service industry supply chains, making them more efficient and valuable".split(" ");

const inView = ref(false);
const header = ref<HTMLElement | null>(null);
let observer: IntersectionObserver | undefined; // Observer initialized without null

const createObserver = () => {
  observer = new IntersectionObserver(
  (entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        inView.value = true;
      }
    });
  },
  {
    root: null, // Use the viewport as the root
    rootMargin: "0px 0px 0px 0px", // Adjust to ensure the entire element is fully in view
    threshold: 0.5, // Trigger when 50% of the element is in view
  }
);
  if (header.value) {
    observer.observe(header.value);
  }
};

onMounted(() => {
  createObserver();
});

onBeforeUnmount(() => {
  if (observer && header.value) {
    observer.disconnect();
  }
});
</script>

<style>
h1 {
  display: inline-block;
  vertical-align: top;
  text-decoration: inherit;
  text-wrap: balance;
  line-height: 1.1;
  font-weight: 538;
  font-variation-settings: "opsz" 28;
  margin-block-start: 0.83em;
  margin-block-end: 0.83em;
}

span {
  display: inline-block;
  line-height: inherit;
  will-change: auto;
  margin-right: 4px;
  word-spacing: 0.25em; /* Adjust space between words globally */
}
</style>
