<template>
  <section id="work" class="bg-base py-32 px-6">
    <div class="max-w-6xl mx-auto">

      <p class="label text-mauve mb-4">Work History</p>
      <h2 class="font-display text-3xl md:text-4xl font-bold text-text mb-6 leading-tight">
        Where I've been,<br />
        <span class="text-mauve">and what I built.</span>
      </h2>
      <p class="text-subtext0 leading-relaxed mb-24 max-w-xl">
        Every role shaped how I work today — from early freelance projects to owning
        the full implementation lifecycle at scale.
      </p>

      <div class="relative">
        <div class="hidden md:block absolute left-1/2 -translate-x-1/2 top-0 bottom-0 w-px bg-surface1"></div>

        <div class="flex flex-col gap-16">
          <div
            v-for="(job, index) in jobs"
            :key="job.company"
            class="relative grid md:grid-cols-2 gap-8 md:gap-16 items-start"
          >
            <div class="hidden md:flex absolute left-1/2 -translate-x-1/2 w-3 h-3 rounded-full bg-mauve border-2 border-base z-10 top-8"></div>

            <div :class="index % 2 === 0 ? 'md:text-right md:pr-12' : 'md:order-2 md:pl-12'">
              <h3 class="font-display text-xl font-bold text-text mb-3">
                <a :href="job.url" target="_blank" rel="noopener noreferrer" class="hover:text-mauve transition-colors inline-flex items-center gap-2">
                  {{ job.company }}
                  <MoveUpRight class="w-4 h-4" />
                </a>
              </h3>
              <div class="flex flex-col gap-1" :class="index % 2 === 0 ? 'md:items-end' : ''">
                <div v-for="role in job.roles" :key="role.title">
                  <p class="text-mauve text-sm font-medium">{{ role.title }}</p>
                  <p class="label text-overlay1 mb-2">{{ role.period }}</p>
                </div>
              </div>
            </div>

            <div :class="index % 2 === 0 ? 'md:pl-12' : 'md:order-1 md:pr-12'">
              <div class="glow rounded-2xl bg-surface0 border border-surface1 p-6">
                <p class="text-subtext0 leading-relaxed mb-5 text-sm">{{ job.description }}</p>
                <div
                  class="flex flex-wrap gap-2"
                  :class="index % 2 !== 0 ? 'md:justify-end' : ''"
                >
                  <span v-for="tag in job.tags" :key="tag" class="tag">{{ tag }}</span>
                </div>
              </div>
            </div>

          </div>
        </div>
      </div>

      <div class="mt-24 border-t border-surface1 pt-16">
        <button
          @click="systemsOpen = !systemsOpen"
          class="flex items-center gap-4 w-full group"
        >
          <div class="flex-1 text-left">
            <p class="label text-mauve mb-1">Systems I've built integrations with</p>
            <p class="text-subtext0 text-sm">{{ systemsOpen ? 'Click to collapse' : `${totalSystems} systems across ${integrationCategories.length} categories` }}</p>
          </div>
          <span
            class="text-overlay1 group-hover:text-mauve transition-all duration-200 text-xl"
            :class="systemsOpen ? 'rotate-45' : ''"
          >+</span>
        </button>

        <Transition
          enter-active-class="transition-all duration-300 ease-out"
          enter-from-class="opacity-0 -translate-y-2"
          enter-to-class="opacity-100 translate-y-0"
          leave-active-class="transition-all duration-200 ease-in"
          leave-from-class="opacity-100 translate-y-0"
          leave-to-class="opacity-0 -translate-y-2"
        >
          <div v-if="systemsOpen" class="mt-10 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
            <div
              v-for="category in integrationCategories"
              :key="category.name"
              class="rounded-2xl bg-surface0 border border-surface1 p-6"
            >
              <p class="label text-overlay1 mb-4">{{ category.name }}</p>
              <div class="flex flex-wrap gap-2">
                <span v-for="system in category.systems" :key="system" class="tag">{{ system }}</span>
              </div>
            </div>
          </div>
        </Transition>
      </div>

    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { MoveUpRight } from 'lucide-vue-next'

interface Role {
  title: string
  period: string
}

interface Job {
  company: string
  url: string
  roles: Role[]
  description: string
  tags: string[]
}

interface IntegrationCategory {
  name: string
  systems: string[]
}

export default defineComponent({
  components: { MoveUpRight },
  data() {
    return {
      systemsOpen: false,

      jobs: [
        {
          company: 'Learningbank',
          url: 'https://learningbank.io',
          roles: [
            { title: 'Technical Solutions Engineer', period: 'Oct 2025 – Present' },
            { title: 'Integration Developer', period: 'Sep 2023 – Oct 2025' },
          ],
          description: 'The role where I stopped being just a developer and started owning the entire journey. From sitting in sales meetings to building the integration to being on the call when something breaks — I\'m in every stage, every time. I\'ve expanded the Integration Hub, built a public-facing API, and developed custom automations for a wide range of customer systems.',
          tags: ['TypeScript', 'Vue', 'REST APIs', 'Make.com', 'Customer onboarding', 'Full lifecycle'],
        },
        {
          company: 'Axion',
          url: 'https://axion.io',
          roles: [
            { title: 'Technical Lead (Master Thesis)', period: 'Feb 2025 – Jul 2025' },
          ],
          description: 'Joined the founding team of a Danish DTU startup as part of my master thesis. I led the full technical design and implementation — architecting the Android app in Kotlin, designing the cloud backend in C#/.NET on Azure, setting up the database, CI/CD pipelines, error monitoring and analytics. Defined the entire tech stack from scratch.',
          tags: ['Kotlin', 'C# / .NET', 'Azure', 'REST API', 'MySQL', 'GitHub Actions'],
        },
        {
          company: 'SkanCode A/S',
          url: 'https://skancode.dk',
          roles: [
            { title: 'Software Developer', period: 'Nov 2022 – May 2023' },
          ],
          description: 'Built REST API integrations in Java Spring Boot on AWS, connecting third-party services like GLS and financial platforms to a low-code system. Designed and maintained T-SQL databases, collaborated with stakeholders to scope projects and delivered tailored integration solutions that bridged hardware, software and external systems.',
          tags: ['Java Spring Boot', 'AWS', 'REST APIs', 'T-SQL', 'JavaScript'],
        },
        {
          company: 'Reinhardt Dans',
          url: 'https://reinhardtdans.dk',
          roles: [
            { title: 'Website Developer', period: 'May 2021 – Jan 2022' },
          ],
          description: 'Designed and built a custom WordPress site for a dance school — custom theme, tailored plugins, responsive design, contact forms and SEO setup. Also provided ongoing maintenance and trained the administrators on managing the CMS themselves. My first real taste of owning a project end to end.',
          tags: ['WordPress', 'PHP', 'JavaScript', 'CSS', 'SEO'],
        },
      ] as Job[],

      integrationCategories: [
        {
          name: 'HRIS / ATS / People systems',
          systems: ['Personio', 'CatalystOne', 'HaileyHR', 'Talent Tech', 'Sage People', 'SuccessFactors', 'SameSystem', 'Agresso', 'Microsoft Entra / AD'],
        },
        {
          name: 'Communication & engagement',
          systems: ['Microsoft Teams', 'Microsoft Outlook', 'Relesys', 'Ziik', 'EkkoApp', 'Intercom'],
        },
        {
          name: 'CRM & sales',
          systems: ['HubSpot', 'Plecto'],
        },
        {
          name: 'Project & operations',
          systems: ['Linear', 'Landax'],
        },
        {
          name: 'Finance & logistics',
          systems: ['E-Conomic', 'GLS'],
        },
        {
          name: 'Automation & low-code',
          systems: ['Make.com', 'AWS S3', 'Azure', 'Caspio'],
        },
        {
          name: 'Product API',
          systems: ['Learningbank'],
        },
      ] as IntegrationCategory[],
    }
  },

  computed: {
    totalSystems(): number {
      return this.integrationCategories.reduce((sum, cat) => sum + cat.systems.length, 0)
    },
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
  background: var(--color-surface1);
  color: var(--color-subtext1);
  border: 1px solid var(--color-surface2);
}
</style>
