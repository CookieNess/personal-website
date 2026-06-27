<template>
  <section id="projects" class="bg-base py-32 px-6">
    <div class="max-w-6xl mx-auto">

      <p class="label text-mauve mb-4">Work I'm proud of</p>
      <h2 class="font-display text-3xl md:text-4xl font-bold text-text mb-6 leading-tight">
        Things I've built<br />
        <span class="text-mauve">that actually mattered.</span>
      </h2>
      <p class="text-subtext0 leading-relaxed mb-16 max-w-xl">
        Some for customers, some for fun. All of them built with care.
      </p>

      <div class="flex gap-3 mb-12">
        <button
          v-for="tab in tabs"
          :key="tab.id"
          @click="activeTab = tab.id"
          class="label px-4 py-2 rounded-md transition-all"
          :class="activeTab === tab.id
            ? 'bg-mauve text-crust'
            : 'text-overlay1 hover:text-text border border-surface1 hover:border-mauve'"
        >
          {{ tab.label }}
        </button>
      </div>

      <Transition
        enter-active-class="transition-opacity duration-200"
        enter-from-class="opacity-0"
        enter-to-class="opacity-100"
        mode="out-in"
      >
        <div v-if="activeTab === 'cases'" key="cases" class="flex flex-col gap-6">
          <div
            v-for="(item, index) in customerCases"
            :key="item.title"
            class="rounded-2xl bg-surface0 border border-surface1 p-8 grid md:grid-cols-[1fr_2fr] gap-8 items-start"
          >
            <div>
              <p class="label text-mauve mb-2">Case {{ index + 1 }}</p>
              <h3 class="font-display text-lg font-bold text-text mb-2">{{ item.title }}</h3>
              <p class="label text-overlay1">{{ item.industry }}</p>
            </div>
            <div>
              <div class="flex flex-col gap-4 mb-6">
                <div>
                  <p class="label text-overlay1 mb-2">The problem</p>
                  <p class="text-subtext0 text-sm leading-relaxed">{{ item.problem }}</p>
                </div>
                <div>
                  <p class="label text-overlay1 mb-2">What I built</p>
                  <p class="text-subtext0 text-sm leading-relaxed">{{ item.solution }}</p>
                </div>
                <div>
                  <p class="label text-overlay1 mb-2">The outcome</p>
                  <p class="text-text text-sm leading-relaxed">{{ item.outcome }}</p>
                </div>
              </div>
              <div class="flex flex-wrap gap-2">
                <span v-for="tag in item.tags" :key="tag" class="tag">{{ tag }}</span>
              </div>
            </div>
          </div>
        </div>

        <div v-else key="projects" class="grid md:grid-cols-2 gap-6">
          <div
            v-for="project in personalProjects"
            :key="project.title"
            class="rounded-2xl bg-surface0 border border-surface1 p-6 flex flex-col gap-4"
          >
            <div class="flex items-start justify-between gap-4">
              <h3 class="font-display text-lg font-bold text-text">{{ project.title }}</h3>
              <a
                :href="project.url"
                target="_blank"
                rel="noopener noreferrer"
                class="label text-overlay1 hover:text-mauve transition-colors shrink-0 flex items-center gap-1"
              >
                GitHub ↗
              </a>
            </div>
            <p class="text-subtext0 text-sm leading-relaxed flex-1">{{ project.description }}</p>
            <div class="flex flex-wrap gap-2">
              <span v-for="tag in project.tags" :key="tag" class="tag">{{ tag }}</span>
            </div>
          </div>
        </div>
      </Transition>

    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

interface CustomerCase {
  title: string
  industry: string
  problem: string
  solution: string
  outcome: string
  tags: string[]
}

interface PersonalProject {
  title: string
  description: string
  url: string
  tags: string[]
}

interface Tab {
  id: string
  label: string
}

export default defineComponent({
  data() {
    return {
      activeTab: 'cases',

      tabs: [
        { id: 'cases', label: 'Customer cases' },
        { id: 'projects', label: 'Personal projects' },
      ] as Tab[],

      customerCases: [
        {
          title: 'Centralised integration across 17 factories',
          industry: 'International manufacturing',
          problem: 'A global company needed all users — white collar and blue collar — on the platform. Their headquarters ran a standardised HRIS, but 17 factories across the world each ran something different: different HR systems, different formats, some just an Excel sheet.',
          solution: 'Built a centralised integration running on an SFTP server where all 17 factories could upload their files. Files were automatically processed into standardised user records and synced to the platform — creating, updating and deactivating users as needed. This ran alongside a separate Microsoft Entra integration handling the white collar workforce.',
          outcome: 'Administrators no longer had to manually manage users across 17 locations. Each factory uploads their file, the rest is automatic.',
          tags: ['SFTP', 'Microsoft Entra', 'User sync', 'Multi-system integration', 'Automation'],
        },
        {
          title: 'Building a department hierarchy from incomplete data',
          industry: 'International retailer',
          problem: 'A complex organisation with headquarters, regions, cost centres and departments had severely limited data in their Microsoft Entra. The missing structure meant they couldn\'t use large parts of the platform. The customer was frustrated — they understood the root cause was their own data, but still needed a solution.',
          solution: 'Built an integration that automatically constructed the full department hierarchy from the available Entra data. Where data was missing — regions, sub-departments, etc. — complex rules filled the gaps. The final structure was roughly 50% their real data and 50% derived logic, but the result was a complete, accurate hierarchy.',
          outcome: 'The company could suddenly use automations and features that were previously impossible due to the incomplete setup. A frustrating situation turned into a platform they could actually rely on.',
          tags: ['Microsoft Entra', 'Hierarchy building', 'Data transformation', 'Complex rule engine'],
        },
        {
          title: 'Co-architecting a public-facing API',
          industry: 'Internal platform — Learningbank',
          problem: 'Customers who wanted to build their own integrations with the platform had no good way to do so — there were no up-to-date public endpoints. The options were either pay for a custom integration, try to use the old broken endpoints or go without it.',
          solution: 'Co-architected with the lead developer and built the entire public facing API in TypeScript. Designed the endpoints, defined the data contracts, and built the infrastructure customers needed to pull data and build their own integrations independently.',
          outcome: 'Customers gained full self-service integration capability. A platform limitation became a platform strength.',
          tags: ['TypeScript', 'API design', 'REST', 'Architecture', 'Developer experience'],
        },
      ] as CustomerCase[],

      personalProjects: [
        {
          title: 'This website',
          description: 'Built from scratch in Vue 3 and TypeScript, styled with Tailwind CSS and the Catppuccin Mocha palette. Designed and developed end to end — because if you\'re going to talk about building things, you should probably build your own portfolio.',
          url: 'https://github.com/frederik-kjaergaard/personal-website',
          tags: ['Vue 3', 'TypeScript', 'Tailwind CSS'],
        },
        {
          title: 'Sorting Shenanigans',
          description: 'A visualiser for sorting algorithms — the serious ones and the joke ones. Watch Bubble Sort, Merge Sort and Quicksort do their thing, or let Stalin Sort simply remove any element that isn\'t in order. Each algorithm comes with a plain-English explanation and time complexity breakdown. Because sorting algorithms are more fun when Sleep Sort is in the mix.',
          url: 'https://github.com/frederik-kjaergaard/sorting-shenanigans',
          tags: ['Algorithms', 'Visualisation', 'JavaScript', 'Stalin Sort'],
        },
      ] as PersonalProject[],
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
  background: var(--color-surface1);
  color: var(--color-subtext1);
  border: 1px solid var(--color-surface2);
}
</style>
