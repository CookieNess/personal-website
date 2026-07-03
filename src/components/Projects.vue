<template>
  <section id="projects" class="bg-mantle py-32 px-6">
    <div class="max-w-6xl mx-auto">

      <p class="label text-mauve mb-4">Projects</p>
      <h2 class="font-display text-3xl md:text-4xl font-bold text-text mb-6 leading-tight">
        Things I have built<br />
        <span class="text-mauve">that actually mattered.</span>
      </h2>
      <p class="text-subtext0 leading-relaxed mb-16 max-w-xl">
        Some of it paid, some of it just because I wanted to. All of it mine.
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
            class="glow rounded-2xl bg-surface0 border border-surface1 p-8 grid md:grid-cols-[1fr_2fr] gap-8 items-start"
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
            class="glow rounded-2xl bg-surface0 border border-surface1 p-6 flex flex-col gap-4"
          >
            <div class="flex items-start justify-between gap-4">
              <h3 class="font-display text-lg font-bold text-text">{{ project.title }}</h3>
              <a
                :href="project.url"
                target="_blank"
                rel="noopener noreferrer"
                class="label text-overlay1 hover:text-mauve transition-colors shrink-0 flex items-center gap-1"
              >
                <template v-if="project.isPdf">
                  PDF <FileText class="w-5 h-5" />
                </template>
                <template v-else>
                  Github <Github class="w-5 h-5" />
                </template>
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
import { Github, FileText } from 'lucide-vue-next'

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
  isPdf?: boolean
}

interface Tab {
  id: string
  label: string
}

export default defineComponent({
  components: {
    Github,
    FileText,
  },
  data() {
    return {
      activeTab: 'cases',

      tabs: [
        { id: 'cases', label: 'Customer cases' },
        { id: 'projects', label: 'Personal projects' },
      ] as Tab[],

      customerCases: [
        {
          title: 'Centralised Integration Across 17 Factories',
          industry: 'International Manufacturing Company',
          problem: 'A global company needed all users, white and blue collar, on their platform. Their headquarters ran a standardised HRIS, but 17 factories across the world each ran something different: different HR systems, different formats, some just an Excel sheet.',
          solution: 'Built a centralised integration running on an SFTP server where all 17 factories could upload CSV files for the blue collar workers. Files were automatically processed into standardised user records and synced to their platform, automatically creating, updating and deactivating users as needed. This ran alongside a separate Microsoft Entra integration handling the white collar workforce.',
          outcome: 'Administrators no longer had to manually manage users across 17 locations. Each factory uploads their file and the rest is handled automatically.',
          tags: [],
        },
        {
          title: 'Building A Department Hierarchy From Incomplete Data',
          industry: 'International retailer',
          problem: 'A complex organisation with headquarters, regions, cost centres, departments, etc., had severely limited data in their Microsoft Entra. The missing structure meant they could not utilize their platform effectively. The customer was frustrated. They understood the root cause was their own data, but still needed a solution.',
          solution: 'Built an integration that automatically constructed the full department hierarchy from the available Entra data. Where data was missing, complex rules filled the gaps, to keep it automated. The final structure was roughly 50% their real data and 50% derived logic, but the result was a complete, accurate hierarchy.',
          outcome: 'The company could use automations and features that were previously difficult to use due to the incomplete setup. A frustrating situation turned into a platform they could actually rely on.',
          tags: [],
        },
        {
          title: 'Co-architecting A Public Facing API',
          industry: 'Internal platform - Learningbank',
          problem: 'Customers who wanted to build their own integrations with the platform had no good way to do so. There were no up-to-date public endpoints. The options were either: pay for a custom integration, try to use the old broken endpoints or simply go without it.',
          solution: 'Co-architected with the lead developer and built the entire public facing API in TypeScript and NestJS. Designed the endpoints, defined the data structures and built the infrastructure customers needed to pull data and build their own integrations independently.',
          outcome: 'Customers gained full self-service integration capability. A platform limitation became a platform strength and selling point.',
          tags: [],
        },
      ] as CustomerCase[],

      personalProjects: [
        {
          title: 'This Website',
          description: 'Built in Vue 3 and TypeScript with Tailwind CSS. Designed together with AI assistance, but every decision, every component and every section shaped and owned by me.',
          url: 'https://github.com/CookieNess/personal-website',
          tags: ['Vue 3', 'TypeScript', 'Tailwind CSS'],
        },
        {
          title: 'Sorting Shenanigans',
          description: 'A visualiser for sorting algorithms: both the serious ones and the joke ones. I have always been a fan of sorting algorithms and trying to figure out the time complexity, of algorithms that should not even exist. This project is a playground for that.',
          url: 'https://github.com/CookieNess/sorting-shenanigans',
          tags: ['Sorting Algorithms', 'Time Complexity', 'TypeScript', 'Vue'],
        },
        {
          title: 'Bachelor Thesis',
          description: 'My bachelor thesis at the Technical University of Denmark (DTU) in Computer Science & Engineering. I, together with my project partner, built a system to track and visualise your portfolio. First limited to stocks, but designed to be extended to any form of asset. The project landed us a 10, or B, grade. The system is built in Flutter/Dart, C# and T-SQL',
          url: '/pdfs/bachelor_thesis_2023.pdf',
          tags: ['Flutter', 'Dart', 'C#', 'T-SQL'],
          isPdf: true,
        },
        {
          title: 'Master Thesis',
          description: 'My master thesis at the Technical University of Denmark (DTU) in Computer Science & Engineering. I, together with my project partner, built an Android application in Kotlin, that could limit your screen time by blocking apps and websites. My project partner created the company, Axion, where I handled most of the technical work. The application is built in Kotlin with a C#/ASP.NET backend and a MySQL database, all running on Azure. Sentry was used for error monitoring and Firebase for analytics. The project landed us a 12, or A, grade.',
          url: '/pdfs/master_thesis_2025.pdf',
          tags: ['Kotlin', 'C#', 'MySQL', 'Azure', 'Sentry', 'Firebase', 'Business development'],
          isPdf: true,
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
