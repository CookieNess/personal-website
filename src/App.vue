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
        <p class="font-mono text-xs tracking-[0.2em] uppercase text-mauve mb-6">
          Technical Solutions Engineer
        </p>

        <h1 class="font-display font-extrabold text-text leading-none mb-6"
            style="font-size: clamp(3rem, 10vw, 6rem); letter-spacing: -0.03em;">
          Frederik Kjærgaard<span class="text-mauve">.</span>
        </h1>

        <p class="text-subtext1 mb-2" style="font-size: clamp(1.1rem, 2.5vw, 1.6rem); font-weight: 300;">
          Most people hand off.
        </p>
        <p class="text-mauve font-semibold mb-10" style="font-size: clamp(1.1rem, 2.5vw, 1.6rem);">
          I don't.
        </p>

        <div class="flex gap-4 justify-center flex-wrap">
          <a
            href="#work"
            class="px-7 py-3 rounded-md bg-mauve text-base font-medium text-crust hover:bg-lavender transition-all hover:-translate-y-0.5 hover:shadow-[0_8px_24px_rgba(203,166,247,0.25)]"
          >
            See my work
          </a>
          <a
            href="#contact"
            class="px-7 py-3 rounded-md border border-surface1 text-mauve font-medium hover:border-mauve transition-all hover:-translate-y-0.5"
          >
            Get in touch
          </a>
        </div>
      </div>

      <div class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 text-overlay0">
        <span class="font-mono text-[0.6rem] tracking-[0.2em] uppercase">scroll</span>
        <div class="w-px h-10 bg-gradient-to-b from-overlay0 to-transparent animate-pulse"></div>
      </div>
    </section>

    <PlaceholderSection section-id="about"        title="About"             :dark="true"  />
    <PlaceholderSection section-id="work"         title="Work History"      :dark="false" />
    <PlaceholderSection section-id="technologies" title="Technologies"      :dark="true"  />
    <PlaceholderSection section-id="projects"     title="Work I'm proud of" :dark="false" />
    <PlaceholderSection section-id="testimonials" title="Testimonials"      :dark="true"  />
    <PlaceholderSection section-id="contact"      title="Contact"           :dark="false" />
  </div>
</template>

<script setup lang="ts">
import NavBar from '@/components/NavBar.vue'
import PlaceholderSection from '@/components/PlaceholderSection.vue'
</script>
