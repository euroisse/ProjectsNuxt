<template>
    <div>
    <button
      :class="[
        'px-4 py-2 border border-black rounded-md duration-300',
        customClass,
      ]"
    >
      {{ content }}
    </button>
</div>
  </template>
  
  <script setup lang="ts">
  defineProps({
    content: {
      type: String,
      required: true,
    },
    customClass: {
      type: String,
      default: '',
    },
  });
  </script>
  