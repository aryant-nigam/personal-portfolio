<template>
  <section id="experience" class="position-relative z-1 mx-auto px-4 py-5 mb-5" style="max-width: 1280px;">

    <!-- Header -->
    <div class="d-flex flex-column flex-md-row justify-content-between align-items-start mb-5 pb-4 gap-4">
      <div>
        <div class="d-flex align-items-center gap-2 text-xs fw-bold text-zinc-400 mb-3">
          <div class="bg-zinc-400" style="height: 2px; width: 32px;"></div>
          CAREER
        </div>
        <h2 class="display-3 fw-black text-uppercase tracking-tighter lh-1">
          WORK<br />EXPERIENCE
        </h2>
      </div>
      <div style="max-width: 400px;">
        <p class="text-zinc-500 fs-6 leading-relaxed mb-0">
          Building production systems and leading engineering teams — here's where I've done it.
        </p>
      </div>
    </div>

    <!-- Accordion with Stepper Look -->
    <div class="accordion accordion-flush" id="experienceAccordion">
      <div 
        v-for="(exp, i) in experiences" 
        :key="i" 
        class="accordion-item border-0 d-flex gap-3 gap-md-4"
        :class="{ 'active': openedIndices.has(i) }"
        :ref="(el) => setStepRef(el, i)"
        :data-index="i"
      >
        <!-- Stepper Visuals -->
        <div class="step-left d-flex flex-column align-items-center">
          <div class="step-dot mt-4">
            <div class="step-dot-inner"></div>
          </div>
          <div v-if="i < experiences.length - 1" class="step-line"></div>
        </div>

        <!-- Accordion Content -->
        <div class="flex-grow-1">
          <h2 class="accordion-header">
            <button 
              class="accordion-button bg-transparent shadow-none px-0 py-4 d-flex align-items-center" 
              :class="{ 'collapsed': !openedIndices.has(i) }"
              type="button" 
              @click="toggleIndex(i)"
              :aria-expanded="openedIndices.has(i)"
            >
              <div class="w-100 d-flex flex-column flex-md-row align-items-md-center gap-2 gap-md-4">
                <span class="step-period text-xs fw-black text-uppercase tracking-widest text-zinc-400" style="min-width: 140px;">
                  {{ exp.period }}
                </span>
                <div class="d-flex align-items-center gap-3 flex-wrap flex-md-nowrap">
                  <span class="fw-black fs-4 text-zinc-900">{{ exp.role }}</span>
                  <span class="text-zinc-400 fw-bold">@ {{ exp.company }}</span>
                </div>
              </div>
            </button>
          </h2>
          <div 
            class="accordion-collapse collapse" 
            :class="{ 'show': openedIndices.has(i) }"
          >
            <div class="accordion-body px-0 pt-0 pb-4">
              <ul class="list-unstyled d-flex flex-column gap-3 mb-4">
                <li v-for="(point, j) in exp.bullets" :key="j" class="d-flex align-items-start gap-3">
                  <div class="mt-2 bg-zinc-900 rounded-circle" style="width: 6px; height: 6px; flex-shrink: 0;"></div>
                  <span class="text-zinc-600 fs-6 leading-relaxed">{{ point }}</span>
                </li>
              </ul>
              <div class="d-flex flex-wrap gap-2">
                <span v-for="skill in exp.skills" :key="skill" class="skill-chip rounded-pill text-uppercase">{{ skill }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

  </section>
</template>

<script>
import experiencesData from '../data/experience.json';

export default {
  name: 'Experience',
  data() {
    return {
      openedIndices: new Set([0]),
      stepRefs: [],
      observer: null,
      experiences: experiencesData
    };
  },
  methods: {
    toggleIndex(i) {
      const newIndices = new Set(this.openedIndices);
      if (newIndices.has(i)) {
        newIndices.delete(i);
      } else {
        newIndices.add(i);
      }
      this.openedIndices = newIndices;
    },
    setStepRef(el, i) {
      if (el) {
        this.stepRefs[i] = el;
      }
    }
  },
  mounted() {
    this.observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          const index = parseInt(entry.target.dataset.index);
          const newIndices = new Set(this.openedIndices);
          newIndices.add(index);
          this.openedIndices = newIndices;
        }
      });
    }, {
      threshold: 0.3,
      rootMargin: '0px 0px -20% 0px'
    });

    this.stepRefs.forEach((el) => {
      if (el) this.observer.observe(el);
    });
  },
  beforeUnmount() {
    if (this.observer) {
      this.observer.disconnect();
    }
  }
}
</script>

<style scoped>
.z-10 { z-index: 10; }
.fw-black { font-weight: 900; }
.text-xs { font-size: 11px; }
.tracking-widest { letter-spacing: 0.1em; }

.accordion-item { background: transparent; }

/* Stepper Visuals */
.step-left { width: 24px; flex-shrink: 0; }
.step-dot {
  width: 24px;
  height: 24px;
  border-radius: 50%;
  border: 2px solid var(--zinc-200);
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--selection-text);
  transition: all 0.3s ease;
  z-index: 2;
}
.step-dot-inner {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--zinc-200);
  transition: all 0.3s ease;
}
.step-line {
  width: 2px;
  flex-grow: 1;
  background: var(--zinc-200);
  margin: 4px 0;
  transition: all 0.4s ease;
}

.accordion-item.active .step-dot { border-color: var(--zinc-900); background: var(--zinc-900); }
.accordion-item.active .step-dot-inner { background: var(--selection-text); }
.accordion-item.active .step-line { background: var(--zinc-900); }

/* Accordion Customization */
.accordion-button::after {
  display: none; /* Remove default arrow */
}

.accordion-button:not(.collapsed) {
  color: var(--zinc-900);
  background-color: transparent;
}

/* Skill chips */
.skill-chip {
  font-size: 10px;
  font-weight: 800;
  letter-spacing: 0.08em;
  padding: 4px 12px;
  background: var(--zinc-100);
  color: var(--zinc-600);
  border: 1px solid var(--zinc-200);
  transition: all 0.2s ease;
}
.skill-chip:hover {
  background: var(--zinc-900);
  color: var(--selection-text);
  border-color: var(--zinc-900);
}
</style>


