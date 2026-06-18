<template>
  <section
    :id="sectionId"
    class="min-h-screen flex items-center justify-center border-b border-surface0"
    :class="dark ? 'bg-mantle' : 'bg-base'"
  >
    <div class="text-center">
      <p class="font-mono text-xs tracking-widest uppercase text-overlay0 mb-3">Coming soon</p>
      <h2 class="font-display text-3xl font-bold text-text">{{ title }}</h2>
    </div>
  </section>
</template>

<script setup lang="ts">
defineProps<{
  sectionId: string
  title: string
  dark?: boolean
}>()
</script>
