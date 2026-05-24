<template>
  <section id="stack" class="position-relative z-1 mx-auto px-4 py-5 mb-5" style="max-width: 1400px;">
    
    <div class="row g-0">
      <!-- Side Indicator Column -->
      <div class="col-auto d-none d-xl-flex flex-column align-items-center pt-5 pe-5 position-relative" style="min-width: 160px;">
        <div 
          class="scroll-down-wrapper d-flex flex-column align-items-center transition-transform-smooth"
          :style="{ transform: `translateY(${indicatorOffset}px)` }"
        >
          <div class="scroll-down-text text-uppercase fw-bold text-zinc-400 mb-4">
            {{ isAllRevealed ? 'Back to Top' : 'Discover More' }}
          </div>
          <div class="scroll-line mb-4"></div>
          <button 
            @click="handleNavigation"
            class="scroll-circle d-flex align-items-center justify-content-center bg-black border-0 cursor-pointer transition-base hover-scale"
            :aria-label="isAllRevealed ? 'Scroll to Top' : 'Next Row'"
          >
            <ArrowDownIcon size="16" class="text-white arrow-anim" :class="{ 'rotate-180': isAllRevealed }" />
          </button>
        </div>
      </div>

      <!-- Main Content -->
      <div class="col">
        <!-- Header -->
        <div class="d-flex flex-column flex-md-row justify-content-between align-items-start align-items-md-end mb-5 pb-4 gap-4 header-anchor">
          <div>
            <div class="d-flex align-items-center gap-2 text-xs fw-bold text-zinc-500 mb-3">
              <div class="bg-zinc-300" style="height: 1px; width: 40px;"></div>
              EXPERTISE
            </div>
            <h2 class="display-3 fw-black text-uppercase tracking-tighter lh-1 text-black">
              TECH STACK<br />& SERVICES
            </h2>
          </div>
          <div style="max-width: 420px;" class="pb-2">
            <p class="text-zinc-500 fs-6 leading-relaxed mb-0">
              Transforming complex requirements into seamless digital solutions using a modern, high-performance toolkit.
            </p>
          </div>
        </div>

        <!-- Tech Grid with Transition -->
        <div class="tech-grid-container position-relative">
          <transition-group 
            name="grid-fade" 
            tag="div" 
            class="row g-4 py-2 overflow-hidden"
          >
            <div 
              v-for="(skill, i) in visibleSkills" 
              :key="skill.name" 
              class="col-12 col-md-6 col-lg-3 tech-card-wrapper"
              :ref="(el) => setCardRef(el, i)"
            >
             <div 
                class="tech-card-flip"
                :class="{ 'is-flipped': flippedCards.has(i) }"
                @click="toggleFlip(i)"
                @mouseenter="hoveredCard = i"
                @mouseleave="hoveredCard = null"
              >
                <!-- Front -->
                <div class="flip-card-front p-4 bg-black text-white border border-zinc-800 d-flex flex-column gap-4">
                  <div 
                    class="tech-icon-box d-flex justify-content-center align-items-center w-100"
                    :style="{
                      color: hoveredCard === i ? skill.color : '#ffffff'
                    }"
                  >
                    <SvgIcon :name="skill.icon" size="56" stroke-width="1" />
                  </div>
                  
                  <div class="mt-auto">
                    <h3 class="fw-black text-uppercase tracking-tight mb-3" style="font-size: 1.25rem; line-height: 1.1;">
                      {{ skill.name }}
                    </h3>
                    <p class="text-xs text-uppercase fw-bold opacity-60 mb-4 letter-spacing-lg">
                      {{ skill.desc }}
                    </p>
                    
                    <div class="d-flex align-items-center gap-3 read-more cursor-pointer">
                      <span class="text-xs fw-black text-uppercase tracking-widest">Click to explore</span>
                      <ArrowRightIcon size="14" class="arrow-icon" />
                    </div>
                  </div>
                </div>

                <!-- Back -->
                <div class="flip-card-back p-4 bg-black text-white border border-zinc-800 d-flex flex-column justify-content-center">
                  <h4 class="fw-black text-uppercase tracking-tight mb-3" style="font-size: 0.9rem;">Used in:</h4>
                  <ul class="list-unstyled d-flex flex-column gap-2">
                    <li v-for="(usage, j) in skill.usedIn" :key="j" class="d-flex align-items-start gap-2 text-xs">
                      <span class="badge bg-white text-black fw-bold flex-shrink-0">✓</span>
                      <span class="flex-grow-1">{{ usage }}</span>
                    </li>
                  </ul>
                  <div class="d-flex align-items-center gap-2 mt-4 cursor-pointer" style="opacity: 0.6;">
                    <ArrowRightIcon size="12" class="rotate-180" />
                    <span class="text-xs fw-bold">Back</span>
                  </div>
                </div>
              </div>
            </div>
          </transition-group>
        </div>

        <div class="d-flex justify-content-center mt-4 d-xl-none">
          <button
            @click="handleNavigation"
            class="mobile-nav-button d-flex align-items-center justify-content-center bg-black text-white border-0 rounded-circle"
            :aria-label="isAllRevealed ? 'Scroll to Top' : 'Next Row'"
          >
            <ArrowDownIcon size="18" class="mobile-arrow" :class="{ 'rotate-180': isAllRevealed }" />
          </button>
        </div>
      </div>
    </div>

  </section>
</template>

<script>
import { nextTick } from 'vue';
import skillsData from '../data/skills.json';
import SvgIcon from './SvgIcon.vue';
import { ArrowDownIcon, ArrowRightIcon } from 'lucide-vue-next';

export default {
  name: 'Services',
  components: {
    ArrowDownIcon,
    ArrowRightIcon,
    SvgIcon
  },
  data() {
    return {
      skills: skillsData,
      visibleRowsCount: 1,
      itemsPerRow: 4,
      cardRefs: [],
      indicatorOffset: 0,
      flippedCards: new Set(),
      hoveredCard: null
    };
  },
  computed: {
    visibleSkills() {
      const limit = this.visibleRowsCount * this.itemsPerRow;
      return this.skills.slice(0, limit);
    },
    isAllRevealed() {
      return this.visibleRowsCount * this.itemsPerRow >= this.skills.length;
    }
  },
  methods: {
    setCardRef(el, index) {
      if (el) {
        this.cardRefs[index] = el;
      }
    },
    toggleFlip(index) {
      const newFlipped = new Set(this.flippedCards);
      if (newFlipped.has(index)) {
        newFlipped.delete(index);
      } else {
        newFlipped.add(index);
      }
      this.flippedCards = newFlipped;
    },
    async handleNavigation() {
      if (this.isAllRevealed) {
        const section = document.getElementById('stack');
        if (section) {
          section.scrollIntoView({ behavior: 'smooth' });
        }
      } else {
        const oldIndex = this.visibleSkills.length;
        this.visibleRowsCount++;
        
        await nextTick();
        
        if (this.cardRefs[oldIndex]) {
          const cardEl = this.cardRefs[oldIndex];
          const gridContainer = cardEl.offsetParent;
          
          if (gridContainer) {
            this.indicatorOffset = cardEl.offsetTop + gridContainer.offsetTop;
          }

          cardEl.scrollIntoView({ behavior: 'smooth', block: 'center' });
        }
      }
    }
  }
}
</script>

<style scoped>
.fw-black { font-weight: 900; }
.text-xs { font-size: 11px; }
.letter-spacing-lg { letter-spacing: 0.1em; }
.cursor-pointer { cursor: pointer; }

/* Side Indicator */
.scroll-down-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
}

.transition-transform-smooth {
  transition: transform 0.6s cubic-bezier(0.23, 1, 0.32, 1);
}

.scroll-down-text {
  writing-mode: vertical-rl;
  transform: rotate(180deg);
  font-size: 10px;
  letter-spacing: 0.3em;
  white-space: nowrap;
}

.scroll-line {
  width: 1px;
  height: 80px;
  background: var(--selection-bg);
}

.scroll-circle {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  transition: all 0.3s ease;
}

.hover-scale:hover {
  transform: scale(1.1);
  background-color: var(--zinc-800) !important;
}

.arrow-anim {
  transition: transform 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.rotate-180 {
  transform: rotate(180deg);
}

/* Tech Card */
.tech-card-wrapper {
  aspect-ratio: 1 / 1.15;
  perspective: 1000px;
}

.tech-icon-box {
  transition: color 0.3s ease;
}

.tech-card-flip {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  transform-style: preserve-3d;
  cursor: pointer;
}

.tech-card-flip.is-flipped {
  transform: rotateY(180deg);
}

.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  border-radius: 24px;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  top: 0;
  left: 0;
}

.flip-card-front {
  z-index: 2;
}

.flip-card-back {
  transform: rotateY(180deg);
  z-index: 1;
}

.tech-card-flip:hover .flip-card-front,
.tech-card-flip:hover .flip-card-back {
  border-color: var(--selection-text) !important;
}

.shadow-sm {
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08) !important;
}

.rotate-180 {
  transform: rotate(180deg);
}


  .mobile-nav-button {
    width: 54px;
    height: 54px;
    box-shadow: 0 10px 28px rgba(0, 0, 0, 0.16);
    transition: transform 0.2s ease, background-color 0.2s ease;
  }

  .mobile-nav-button:hover {
    transform: scale(1.05);
    background-color: var(--zinc-900);
  }

  .mobile-arrow {
    transition: transform 0.35s ease;
  }


.grid-fade-enter-from {
  opacity: 0;
  transform: translateY(30px);
}

.grid-fade-leave-to {
  opacity: 0;
  transform: translateY(-30px);
}

.grid-fade-move {
  transition: transform 0.6s ease;
}

.read-more {
  opacity: 0.8;
  transition: all 0.3s ease;
}

.read-more:hover {
  opacity: 1;
  gap: 20px !important;
}

.arrow-icon {
  transition: transform 0.3s ease;
}

.read-more:hover .arrow-icon {
  transform: translateX(5px);
}

@media (max-width: 1199px) {
  .tech-card-wrapper {
    aspect-ratio: auto;
    min-height: 400px;
  }
}

@media (max-width: 768px) {
  .display-3 { font-size: 3rem; }
  .tech-card { padding: 1.75rem !important; border-radius: 20px; }
}
</style>
