<template>
  <section id="about" class="bg-mantle py-32 px-6">
    <div class="max-w-6xl mx-auto">

      <p class="label text-mauve mb-12">About</p>

      <div class="grid md:grid-cols-2 gap-12 md:gap-16 items-center mb-24">
        <div class="order-2 md:order-1">
          <h2 class="font-display text-3xl md:text-4xl font-bold text-text mb-6 leading-tight">
            Lorem ipsum dolor sit amet,<br />
            <span class="text-mauve">consectetur adipiscing elit.</span>
          </h2>
          <p class="text-subtext0 leading-relaxed mb-4">
            Lorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor
            incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam quis
            nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
          </p>
          <p class="text-subtext0 leading-relaxed">
            Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore
            eu fugiat nulla pariatur excepteur sint occaecat cupidatat non proident,
            sunt in culpa qui officia deserunt mollit anim id est laborum.
          </p>
        </div>

        <div class="order-1 md:order-2">
          <div class="aspect-[4/5] rounded-2xl bg-surface0 border border-surface1 flex items-center justify-center overflow-hidden">
            <img src="@/assets/images/main.png" alt="Frederik Kjærgaard" class="w-full h-full object-cover" />
          </div>
        </div>
      </div>

      <div class="rounded-2xl bg-surface0 border border-surface1 p-8 md:p-12 mb-20">
        <div class="grid md:grid-cols-2 gap-8 items-stretch">

          <div class="md:border-r md:border-surface1 md:pr-8">
            <span class="label inline-block px-3 py-1 rounded-full bg-blue/10 text-blue border border-blue/25 mb-4">
              ↓ technical
            </span>
            <p class="text-subtext0 leading-relaxed">
              Lorem ipsum dolor sit amet consectetur adipiscing elit, sed do eiusmod
              tempor incididunt ut labore et dolore magna aliqua ut enim ad minim veniam.
            </p>
          </div>

          <div>
            <span class="label inline-block px-3 py-1 rounded-full bg-mauve/10 text-mauve border border-mauve/25 mb-4">
              ↓ what it means
            </span>
            <p class="text-text leading-relaxed">
              Lorem ipsum dolor sit amet, this is the plain-English version that
              anyone — technical or not — would understand immediately.
            </p>
          </div>

        </div>
      </div>

      <div>
        <h3 class="font-display text-xl font-semibold text-text mb-6">
          Lorem ipsum, fluent in both
        </h3>
        <div class="grid md:grid-cols-2 gap-8">

          <div>
            <p class="label text-overlay1 mb-3">
              Systems & architecture
            </p>
            <div class="flex flex-wrap gap-2">
              <span v-for="tag in systemTags" :key="tag" class="tag">{{ tag }}</span>
            </div>
          </div>

          <div>
            <p class="label text-overlay1 mb-3">
              Tools that run the business
            </p>
            <div class="flex flex-wrap gap-2">
              <span v-for="tag in businessTags" :key="tag" class="tag">{{ tag }}</span>
            </div>
          </div>

        </div>
      </div>

      <div class="mt-20 flex flex-col sm:flex-row gap-6 items-center border-t border-surface1 pt-12">
        <button @click="lightboxOpen = true" class="shrink-0">
          <div class="w-20 h-20 rounded-xl overflow-hidden border border-surface1 hover:border-mauve transition-colors cursor-zoom-in">
            <img src="@/assets/images/dance.jpg" alt="Me at the European Championships" class="w-full h-full object-cover" />
          </div>
        </button>
        <p class="text-subtext0 text-sm leading-relaxed">
          Lorem ipsum dolor sit amet — before integrations, it was choreography.
          Consectetur adipiscing elit, competed at the World Championships as a
          professional dancer, turns out precision under pressure transfers pretty well.
        </p>
      </div>

    </div>
  </section>

  <Transition
    enter-active-class="transition-opacity duration-200"
    enter-from-class="opacity-0"
    enter-to-class="opacity-100"
  >
    <div v-if="lightboxOpen" @click="lightboxOpen = false" class="fixed inset-0 z-50 bg-crust/90 backdrop-blur-sm flex items-center justify-center cursor-zoom-out p-8">
      <img src="@/assets/images/dance.jpg" alt="Me at the European Championships" class="max-w-full max-h-full rounded-2xl object-contain shadow-2xl" />
    </div>
  </Transition>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  data() {
    return {
      lightboxOpen: false,
      systemTags: [
        'REST & GraphQL APIs',
        'Microservices vs. monolith',
        'Webhooks & event-driven design',
        'OAuth2 & auth flows',
        'Vue & TypeScript',
        'Relational data modelling',
      ],
      businessTags: [
        'HubSpot',
        'Intercom',
        'Make.com',
        'Stakeholder workshops',
        'Requirements gathering',
        'Customer onboarding',
      ],
    }
  },
})
</script>

<style scoped>
.tag {
  font-family: var(--font-mono);
  font-size: 0.7rem;
  letter-spacing: 0.02em;
  padding: 0.35rem 0.75rem;
  border-radius: 999px;
  background: var(--color-surface0);
  color: var(--color-subtext1);
  border: 1px solid var(--color-surface1);
}
</style>