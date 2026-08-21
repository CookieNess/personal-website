<template>
  <div class="min-h-screen bg-base text-text">
    <NavBar />

    <section class="relative min-h-screen flex items-center justify-center overflow-hidden">

      <div
        class="absolute inset-0 opacity-[0.07]"
        style="
          background-image: radial-gradient(var(--color-surface1) 1px, transparent 1px);
          background-size: 32px 32px;
          mask-image: radial-gradient(ellipse 80% 80% at 50% 50%, black 30%, transparent 100%);
        "
      ></div>

      <div
        class="absolute w-[600px] h-[600px] rounded-full pointer-events-none"
        style="
          background: radial-gradient(circle, rgba(203,166,247,0.08) 0%, transparent 70%);
          top: 50%; left: 50%;
          transform: translate(-50%, -50%);
        "
      ></div>

      <div class="relative z-10 text-center px-6 max-w-4xl mx-auto">
        <!-- <p class="font-mono text-xs tracking-[0.2em] uppercase text-mauve mb-6">
          Technical Solutions Engineer
        </p> -->

        <h1 class="font-display font-extrabold text-text leading-none mb-6"
            style="font-size: clamp(3rem, 10vw, 6rem); letter-spacing: -0.03em;">
          Frederik Kjærgaard<span class="text-mauve">.</span>
        </h1>

        <p class="text-subtext1 mb-2" style="font-size: clamp(1.1rem, 2.5vw, 1.6rem); font-weight: 300;">
          Most people hand off a project.
        </p>
        <p class="text-mauve font-semibold mb-10" style="font-size: clamp(1.1rem, 2.5vw, 1.6rem);">
          I do not.
        </p>

        <div class="flex gap-4 justify-center flex-wrap">
          <a
            href="#work"
            class="px-7 py-3 rounded-md bg-mauve text-base font-medium text-crust hover:bg-lavender transition-all hover:-translate-y-0.5 hover:shadow-[0_8px_24px_rgba(203,166,247,0.25)]"
          >
            My work
          </a>
          <a
            href="#connect"
            class="px-7 py-3 rounded-md border border-surface1 text-mauve font-medium hover:border-mauve transition-all hover:-translate-y-0.5"
          >
            Connect
          </a>
        </div>
        <div class="mt-4">
          <a
            href="/pdfs/cv.pdf"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center gap-2 font-mono text-xs tracking-widest uppercase text-overlay1 hover:text-mauve transition-colors"
          >
            <Download class="w-4 h-4"/>
            Download CV
          </a>
        </div>
      </div>


      <div class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 text-overlay0">
        <span class="font-mono text-[0.6rem] tracking-[0.2em] uppercase">scroll</span>
        <div class="w-px h-10 bg-gradient-to-b from-overlay0 to-transparent animate-pulse"></div>
      </div>
      
    </section>

    <AboutSection />
    <WorkHistory />
    <HowIWork />
    <InTheirWords />
    <Projects />
    <Connect />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

import NavBar from '@/components/NavBar.vue'
import AboutSection from '@/components/AboutSection.vue'
import WorkHistory from '@/components/WorkHistory.vue'
import InTheirWords from './components/InTheirWords.vue'
import Connect from './components/Connect.vue'
import HowIWork from './components/HowIWork.vue'
import Projects from './components/Projects.vue'
import { Download } from 'lucide-vue-next'

export default defineComponent({
  components: {
    NavBar,
    AboutSection,
    WorkHistory,
    InTheirWords,
    Connect,
    HowIWork,
    Projects,
    Download,
  },
})
</script>