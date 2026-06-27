<template>
  <section id="connect" class="bg-base py-32 px-6">
    <div class="max-w-6xl mx-auto text-center">

      <p class="label text-mauve mb-4">Connect</p>
      <h2 class="font-display text-3xl md:text-5xl font-bold text-text mb-6 leading-tight">
        Let's connect!
      </h2>
      <p class="text-subtext0 leading-relaxed mb-10 max-w-md mx-auto">
        Want to talk integrations, implementations, or just have a good conversation?
        Find me on LinkedIn.
      </p>

      <a
        href="https://www.linkedin.com/in/frederik-kjaergaard-17a131201/"
        target="_blank"
        rel="noopener noreferrer"
        class="inline-flex items-center gap-3 px-8 py-4 rounded-md bg-mauve text-crust font-medium hover:bg-lavender transition-all hover:-translate-y-0.5 hover:shadow-[0_8px_24px_rgba(203,166,247,0.25)]"
      >
        <Linkedin class="w-5 h-5" />
        Connect on LinkedIn
      </a>

    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { Linkedin } from 'lucide-vue-next'

export default defineComponent({
  components: { Linkedin },
})
</script>
