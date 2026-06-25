<template>
  <header
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
    :class="scrolled ? 'bg-crust/80 backdrop-blur-md border-b border-surface0' : 'bg-transparent'"
  >
    <nav class="max-w-6xl mx-auto px-6 h-16 flex items-center justify-between">

      <a href="#" class="flex items-center">
        <img :src="monogram" alt="Frederik Kjærgaard" class="h-9 w-auto" />
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

<script lang="ts">
import { defineComponent } from 'vue'
import monogram from '@/assets/brand/monogram.png'

interface NavLink {
  href: string
  label: string
}

export default defineComponent({
  data() {
    return {
      monogram,
      scrolled: false,
      menuOpen: false,
      navLinks: [
        { href: '#about', label: 'About' },
        { href: '#work', label: 'Work history' },
        { href: '#technologies', label: 'Tech' },
        { href: '#projects', label: 'Projects' },
        { href: '#testimonials', label: 'Testimonials' },
        { href: '#contact', label: 'Contact' },
      ] as NavLink[],
    }
  },

  mounted() {
    window.addEventListener('scroll', this.onScroll, { passive: true })
    this.onScroll()
  },

  beforeUnmount() {
    window.removeEventListener('scroll', this.onScroll)
  },

  methods: {
    onScroll() {
      this.scrolled = window.scrollY > 24
    },
  },
})
</script>
