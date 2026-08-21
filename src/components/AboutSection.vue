

<template>
  <section id="about" class="bg-mantle py-32 px-6">
    <div class="max-w-6xl mx-auto">

      <p class="label text-mauve mb-12">About</p>

      <div class="grid md:grid-cols-2 gap-12 md:gap-16 items-center mb-24">
        <div class="order-2 md:order-1">
          <h2 class="font-display text-3xl md:text-4xl font-bold text-text mb-6 leading-tight">
            I do not hand off the hard parts,<br />
            <span class="text-mauve">I own them.</span>
          </h2>
          <p class="text-subtext0 leading-relaxed mb-4">
            I am a Technical Solutions Engineer from Denmark with an MSc in Computer Science and Engineering - but the degree is not really the point. <span class="text-mauve font-medium">The point is that I am in the room for every part of an implementation</span> - the sales conversation, the building, the testing, and whatever comes through support after. <span class="text-mauve font-medium">I do not pass the torch. I carry it the whole way.</span>
          </p>
          <p class="text-subtext0 leading-relaxed">
            Yes, I am a software engineer and I can build entire applications, but <span class="text-mauve font-medium">my real expertise is translating complex technical setups into something every stakeholder can understand</span> - whether that is a Head of HR or a die-hard senior engineer.
          </p>
        </div>

        <div class="order-1 md:order-2">
          <div class="aspect-[4/5] rounded-2xl bg-surface0 border border-surface1 flex items-center justify-center overflow-hidden">
            <img src="@/assets/images/main.png" alt="Me celebrating after I finished my masters degree" class="w-full h-full object-cover" />
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
              An OAuth 2.0 connection with Microsoft Entra as the identity provider, calling our REST API endpoints to upsert users with an agreed JSON payload.
            </p>
          </div>

          <div>
            <span class="label inline-block px-3 py-1 rounded-full bg-mauve/10 text-mauve border border-mauve/25 mb-4">
              ↓ what it means
            </span>
            <p class="text-text leading-relaxed">
              A connection with your Microsoft Entra that automatically creates and updates your users on the platform - with exactly the data we agreed on.
            </p>
          </div>

        </div>
      </div>

      <div>
        <h3 class="font-display text-xl font-semibold text-text mb-6">
          A taste of what I work with
        </h3>
        <div class="grid md:grid-cols-2 gap-8">

          <div>
            <p class="label text-overlay1 mb-3">
              Systems & Architecture
            </p>
            <div class="flex flex-wrap gap-2">
              <span v-for="tag in systemTags" :key="tag" class="tag">{{ tag }}</span>
            </div>
          </div>

          <div>
            <p class="label text-overlay1 mb-3">
              Beyond the Code
            </p>
            <div class="flex flex-wrap gap-2">
              <span v-for="tag in businessTags" :key="tag" class="tag">{{ tag }}</span>
            </div>
          </div>

        </div>
      </div>

      <div class="mt-12 border-t border-surface1 pt-12">
        <h3 class="font-display text-xl font-semibold text-text mb-6">Credentials</h3>
        <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
          <a
            v-for="cert in certificates"
            :key="cert.label"
            :href="cert.url"
            :data-umami-event="cert.umamiEvent"
            target="_blank"
            rel="noopener noreferrer"
            class="glow group rounded-2xl bg-surface0 border border-surface1 p-5 flex items-center justify-between gap-4"
          >
            <div>
              <p class="text-text text-sm font-medium leading-snug">{{ cert.label }}</p>
              <p class="label text-overlay1 mt-1">{{ cert.sub }}</p>
            </div>
            <template v-if="cert.type === 'degree'">
              <GraduationCap class="text-overlay1 group-hover:text-mauve w-6 h-6 shrink-0" />
            </template>
            <template v-else>
              <Award class="text-overlay1 group-hover:text-mauve w-6 h-6 shrink-0" />
            </template>
          </a>
        </div>
      </div>

      <div class="mt-20 flex flex-col sm:flex-row gap-6 items-center border-t border-surface1 pt-12">
        <button @click="lightboxOpen = true" class="shrink-0">
          <div class="w-20 h-20 rounded-xl overflow-hidden border border-surface1 hover:border-mauve transition-colors cursor-zoom-in">
            <img src="@/assets/images/dance.jpg" alt="Me at the European Championships" class="w-full h-full object-cover" />
          </div>
        </button>
        <p class="text-subtext0 text-sm leading-relaxed">
          A fact most colleagues find out eventually: before all of this, I was a professional dancer who competed at the European & World Championships. Different kind of choreography these days to be honest, but same obsession with getting the details <span class="text-mauve italic">just</span> right.
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
import { GraduationCap, Award } from 'lucide-vue-next'

interface Certificate {
  label: string
  sub: string
  url: string
  type: 'degree' | 'certificate'
  umamiEvent: string
}

export default defineComponent({
  components: {
    GraduationCap,
    Award,
  },
  data() {
    return {
      lightboxOpen: false,
      systemTags: [
        'REST APIs',
        'Microservices',
        'Vue',
        'TypeScript',
        'NestJS',
        'MySQL',
        'Unit Testing',
        'Linux',
        'Relational Databases',
        'AI-assisted development (Codex, Claude)',
        'Technical diagramming'
      ],
      businessTags: [
        'HubSpot',
        'Intercom',
        'Make',
        'Linear',
        'Customer onboarding',
        'Scope creation & documentation',
        'Pre-sales support',
        'Up-sell collaboration',
        'Technical translation',
        'Project management',
      ],
      certificates: [
        { 
          label: 'BSc in Engineering', 
          sub: 'Software Technology',
          url: 'https://app.diplomasafe.com/en-US/diploma/db79527a2ce1e2e2a0a535b4200117d3fdb1da33a',
          type: 'degree',
          umamiEvent: 'credentials-bsc-degree',
        },
        { 
          label: 'MSc in Engineering', 
          sub: 'Computer Science & Engineering - Software Engineering',
          url: 'https://app.diplomasafe.com/en-US/certificates/d6065cfa3ecceca605ed87d7ef13650cff4ccc716',
          type: 'degree',
          umamiEvent: 'credentials-msc-degree',
        },
        { 
          label: 'Project, Programme and Portfolio Management Diploma', 
          sub: 'ISO 21500 & ISO 21502',
          url: 'https://app.diplomasafe.com/en-US/diploma/d89c0024072e060ca525d4ca0163e3d4b0c49c013',
          type: 'certificate',
          umamiEvent: 'credentials-project-management-diploma',
        },
      ] as Certificate[],
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
