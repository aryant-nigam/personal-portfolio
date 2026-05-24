<template>
  <section
    class="bg-black text-white py-4 position-relative z-3 overflow-hidden skew-y-1 border-top border-bottom border-white border-opacity-10 mt-5"
  >
    <div
      class="animate-marquee d-flex align-items-center gap-5 fs-3 fw-black text-uppercase tracking-tighter fst-italic text-nowrap"
    >
      <div
        v-for="n in 6"
        :key="n"
        class="d-flex align-items-center gap-5"
      >
        <div v-for="highlight in highlights" :key="highlight" class="d-flex align-items-center gap-3">
          <SvgIcon name="SparklesIcon" size="20" class="text-indigo-400" />
          <span>{{ highlight }}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { SparklesIcon } from 'lucide-vue-next';
import SvgIcon from './SvgIcon.vue';
export default {
  name: 'Marquee',
  components: {
    SvgIcon  
  },
  data() {
    return {
      highlights: [
        'Full Stack Engineering',
        'Backend APIs',
        'Cloud Automation',
        'Vue.js & React',
        'AWS Lambda',
        'Workflow Automation',
        'Shopify Integrations',
        'Performance Optimization',
        'SSR Applications',
        'Platform Integrations',
        'Scalable Systems',
        'AI Tools'
      ]
    };
  }
}
</script>

<style scoped>
.fw-black {
  font-weight: 900;
}

.text-indigo-400 {
  color: #a78bfa;
}
</style>