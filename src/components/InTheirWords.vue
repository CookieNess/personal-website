<template>
  <section id="in-their-words" class="bg-base py-32 px-6">
    <div class="max-w-6xl mx-auto">

      <p class="label text-mauve mb-4">In their words</p>
      <h2 class="font-display text-3xl md:text-4xl font-bold text-text mb-6 leading-tight">
        I do not just answer the question.<br />
        <span class="text-mauve">I answer what is behind it.</span>
      </h2>
      <p class="text-subtext0 leading-relaxed mb-16 max-w-xl">
        Most questions carry a concern that nobody actually says out loud. <span class="text-mauve font-medium">Finding that concern, and addressing it, is something I always do.</span> The customers I work with notice it, just as they notice when <span class="text-mauve font-medium">complex technical setups suddenly start making sense to everyone in the room.</span>
      </p>

      <div class="rounded-2xl bg-surface0 border border-surface1 p-8 md:p-12 mb-6">
        <div class="flex items-center gap-3 mb-10">
          <span class="font-display text-lg font-semibold text-text">A real example from a customer</span>
          <div class="h-px flex-1 bg-surface1"></div>
        </div>

        <div class="grid md:grid-cols-2 gap-8 md:gap-16 items-start">

          <div>
            <p class="label text-overlay1 mb-4">What they asked</p>
            <div class="flex flex-col gap-4">
              <div class="bg-base border border-surface1 rounded-tl-sm rounded-tr-2xl rounded-br-2xl rounded-bl-2xl p-4 max-w-s">
                <p class="text-subtext1 text-sm leading-relaxed">Is it possible to set a time limit on the QR code link?</p>
              </div>

              <div class="flex items-center gap-3 py-1">
                <div class="h-px flex-1 bg-surface1"></div>
                <p class="label text-overlay0">literal answer</p>
                <div class="h-px flex-1 bg-surface1"></div>
              </div>

              <div class="bg-red/10 border border-red/20 rounded-tl-sm rounded-tr-2xl rounded-br-2xl rounded-bl-2xl p-4 max-w-s opacity-60">
                <p class="text-red text-sm leading-relaxed">No, that's not possible.</p>
              </div>
            </div>
          </div>

          <div>
            <p class="label text-overlay1 mb-4">What I heard</p>
            <div class="flex flex-col gap-4">
              <div class="bg-base border border-surface1 rounded-tl-sm rounded-tr-2xl rounded-br-2xl rounded-bl-2xl p-4 max-w-s">
                <p class="text-subtext1 text-sm leading-relaxed italic font-semibold">"I'm worried about losing control of who gets into our platform."</p>
              </div>

              <div class="flex items-center gap-3 py-1">
                <div class="h-px flex-1 bg-surface1"></div>
                <p class="label text-overlay0">my answer</p>
                <div class="h-px flex-1 bg-surface1"></div>
              </div>

              <div class="bg-green/10 border border-green/20 rounded-tl-sm rounded-tr-2xl rounded-br-2xl rounded-bl-2xl p-4">
                <p class="text-green text-sm leading-relaxed">That's not possible - but we recommend restricting self sign-up to a specific department with minimum permissions. Other customers do this to stay in full control of exactly who's joining.</p>
              </div>
            </div>
          </div>

        </div>
      </div>

      <div class="flex items-center gap-4 my-16">
        <div class="h-px flex-1 bg-surface1"></div>
        <p class="label text-overlay0">what customers say</p>
        <div class="h-px flex-1 bg-surface1"></div>
      </div>

      <div class="grid md:grid-cols-3 gap-6">
        <div class="glow md:col-span-2 rounded-2xl bg-surface0 border border-mauve/30 p-6 flex flex-col gap-4">
          <p class="text-mauve text-1xl leading-none font-display">// customer</p>
          <p class="text-subtext1 leading-relaxed text-sm flex-1">{{ testimonials[0]!.quote }}</p>
          <p class="label text-overlay1">— {{ testimonials[0]!.role }}</p>
        </div>

        <div class="flex flex-col gap-6">
          <div
            v-for="testimonial in testimonials.slice(1)"
            :key="testimonial.role"
            class="glow rounded-2xl bg-surface0 border border-surface1 p-6 flex flex-col gap-4 flex-1"
          >
            <p class="text-mauve text-1xl leading-none font-display">// customer</p>
            <p class="text-subtext1 leading-relaxed text-sm flex-1">{{ testimonial.quote }}</p>
            <p class="label text-overlay1">— {{ testimonial.role }}</p>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

interface Testimonial {
  quote: string
  role: string
}

export default defineComponent({
  data() {
    return {
      testimonials: [
        {
          quote: 'I just wanted to share how grateful and proud I feel about these past weeks of collaboration. From being lost and a little frustrated, to experiencing smooth collaboration thanks to clarity, quick replies and always kind approach from Frederik. You are a star. We need more people like you who are able to translate IT/developer language to English/business language. Now we also have a clearer picture on what is on our side and yours - and how the integration works.',
          role: 'HR Specialist',
        },
        {
          quote: 'Give Frederik a high five from me - he has a special gift for turning geek into understandable language.',
          role: 'Learning Design and System Manager',
        },
        {
          quote: 'Working together over the past months has honestly been one of the highlights for me - not just because of what we delivered, but because of how we worked together: open, pragmatic and always with a lot of trust and fun.',
          role: 'Project Manager, Digital Solutions',
        },
      ] as Testimonial[],
    }
  },
})
</script>
