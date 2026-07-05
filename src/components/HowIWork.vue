<template>
  <section id="how-i-work" class="bg-mantle py-32 px-6">
    <div class="max-w-6xl mx-auto">

      <p class="label text-mauve mb-4">How I work</p>
      <h2 class="font-display text-3xl md:text-4xl font-bold text-text mb-6 leading-tight">
        Every stage.<br />
        <span class="text-mauve">Every time.</span>
      </h2>
      <p class="text-subtext0 leading-relaxed mb-16 max-w-xl">
        From the first customer conversation to a live implementation, and everything that comes with it.
        <br>
        <span class="text-mauve">I am in every step of the cycle.</span>
        <br><br>
        <span class="italic">And for existing customers, when something changes or an up-sell comes around ... <span class="text-mauve">we go again.</span></span>
      </p>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
        <div
          v-for="(stage, i) in stages"
          :key="stage.title"
          class="glow rounded-2xl bg-surface0 border border-surface1 p-6 flex flex-col gap-3"
        >
          <div
            class="flex items-center justify-between cursor-pointer md:cursor-default"
            @click="toggle(i)"
          >
            <div class="flex items-center gap-3">
              <p class="label text-mauve">{{ String(i + 1).padStart(2, '0') }}</p>
              <h3 class="font-display text-base font-bold text-text">{{ stage.title }}</h3>
            </div>
            <span
              class="md:hidden text-overlay1 transition-transform duration-200"
              :class="openIndex === i ? 'rotate-45' : ''"
            >+</span>
          </div>

          <p
            class="text-subtext0 text-sm leading-relaxed hidden md:block"
            :class="openIndex === i ? '!block' : ''"
          >
            {{ stage.description }}
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

interface Stage {
  title: string
  description: string
}

export default defineComponent({
  data() {
    return {
      openIndex: null as number | null,
      stages: [
        {
          title: 'Pre-sales',
          description: 'I join sales calls when a customer has technical questions - scoping what is possible, identifying opportunities and advising on potential customisations before the deal is done.',
        },
        {
          title: 'Onboarding',
          description: 'Once a customer is signed, I collaborate with the onboarding team and the customer, to make sure the implementation supports how they actually want to work.',
        },
        {
          title: 'Customer alignment',
          description: 'I speak directly with the customer - understanding their setup, their needs, and making sure expectations are clear on both sides before anything gets built.',
        },
        {
          title: 'IT alignment',
          description: 'I get into the technical details with the customer\'s IT team - confirming what is possible on their end before we commit to anything.',
        },
        {
          title: 'Build',
          description: 'I build it. Whether it is a custom implementation or a standard setup, I own what gets delivered.',
        },
        {
          title: 'Verify and test',
          description: 'I test the implementation end to end together with the customer - making sure everything behaves exactly as agreed and expected before it goes live.',
        },
        {
          title: 'Sign-off',
          description: 'When the customer is happy and everything checks out, I close out the implementation. My name is on it and I take responsibility for the outcome.',
        },
        {
          title: 'Support',
          description: 'Bugs and questions do not disappear after it goes live. They come through the support team and land with me - and I make sure they get resolved.',
        },
      ] as Stage[],
    }
  },

  methods: {
    toggle(i: number) {
      this.openIndex = this.openIndex === i ? null : i
      if (this.openIndex !== null) {
        if (!this.stages[i]) {
          return
        }
        window.umami?.track(`how-i-work-stage-${this.stages[i].title.toLowerCase().replace(' ', '-')}`)
      }
    },
  },
})
</script>
