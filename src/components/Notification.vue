<script setup>
  defineProps({
    title: {
      type: String,
      required: true,
    },
  })
</script>
<template>
  <div class="nes-container with-title">
    <p class="title">{{ title }}</p>
    <slot></slot>
  </div>
</template>
