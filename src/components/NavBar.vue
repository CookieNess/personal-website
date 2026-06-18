<template>
  <header
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
    :class="scrolled ? 'bg-crust/80 backdrop-blur-md border-b border-surface0' : 'bg-transparent'"
  >
    <nav class="max-w-6xl mx-auto px-6 h-16 flex items-center justify-between">

      <!-- Logo / name -->
      <a href="#" class="font-display font-bold text-text text-lg tracking-tight hover:text-mauve transition-colors">
        Frederik<span class="text-mauve">.</span>
      </a>

      <!-- Desktop links -->
      <ul class="hidden md:flex items-center gap-8">
        <li v-for="link in navLinks" :key="link.href">
          <a
            :href="link.href"
            class="font-mono text-xs tracking-widest uppercase text-subtext0 hover:text-mauve transition-colors"
          >
            {{ link.label }}
          </a>
        </li>
      </ul>

      <button
        class="md:hidden flex flex-col gap-1.5 p-2 group"
        @click="menuOpen = !menuOpen"
        :aria-expanded="menuOpen"
        aria-label="Toggle menu"
      >
        <span
          class="block w-6 h-px bg-subtext0 transition-all duration-300 group-hover:bg-mauve"
          :class="menuOpen ? 'rotate-45 translate-y-2.5' : ''"
        ></span>
        <span
          class="block w-6 h-px bg-subtext0 transition-all duration-300 group-hover:bg-mauve"
          :class="menuOpen ? 'opacity-0' : ''"
        ></span>
        <span
          class="block w-6 h-px bg-subtext0 transition-all duration-300 group-hover:bg-mauve"
          :class="menuOpen ? '-rotate-45 -translate-y-2.5' : ''"
        ></span>
      </button>
    </nav>

    <Transition
      enter-active-class="transition-all duration-300 ease-out"
      enter-from-class="opacity-0 -translate-y-2"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition-all duration-200 ease-in"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 -translate-y-2"
    >
      <div
        v-if="menuOpen"
        class="md:hidden bg-mantle border-b border-surface0"
      >
        <ul class="max-w-6xl mx-auto px-6 py-6 flex flex-col gap-5">
          <li v-for="link in navLinks" :key="link.href">
            <a
              :href="link.href"
              class="font-mono text-sm tracking-widest uppercase text-subtext0 hover:text-mauve transition-colors"
              @click="menuOpen = false"
            >
              {{ link.label }}
            </a>
          </li>
        </ul>
      </div>
    </Transition>
  </header>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

interface NavLink {
  href: string
  label: string
}

const navLinks: NavLink[] = [
  { href: '#about',         label: 'About' },
  { href: '#work',          label: 'Work history' },
  { href: '#technologies',  label: 'Tech' },
  { href: '#projects',      label: 'Projects' },
  { href: '#testimonials',  label: 'Testimonials' },
  { href: '#contact',       label: 'Contact' },
]

const scrolled = ref(false)
const menuOpen = ref(false)

function onScroll() {
  scrolled.value = window.scrollY > 24
}

onMounted(() => window.addEventListener('scroll', onScroll, { passive: true }))
onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>
