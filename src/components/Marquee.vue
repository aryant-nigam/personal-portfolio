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
        <div class="d-flex align-items-center gap-3">
          <SparklesIcon size="20" class="text-indigo-400" />
          <span>Full Stack Engineering</span>
        </div>

        <div class="d-flex align-items-center gap-3">
          <SparklesIcon size="20" class="text-indigo-400" />
          <span>Backend APIs</span>
        </div>

        <div class="d-flex align-items-center gap-3">
          <SparklesIcon size="20" class="text-indigo-400" />
          <span>Cloud Automation</span>
        </div>

        <div class="d-flex align-items-center gap-3">
          <SparklesIcon size="20" class="text-indigo-400" />
          <span>Vue.js & React</span>
        </div>

        <div class="d-flex align-items-center gap-3">
          <SparklesIcon size="20" class="text-indigo-400" />
          <span>AWS Lambda</span>
        </div>

        <div class="d-flex align-items-center gap-3">
          <SparklesIcon size="20" class="text-indigo-400" />
          <span>Workflow Automation</span>
        </div>

        <div class="d-flex align-items-center gap-3">
          <SparklesIcon size="20" class="text-indigo-400" />
          <span>Shopify Integrations</span>
        </div>

        <div class="d-flex align-items-center gap-3">
          <SparklesIcon size="20" class="text-indigo-400" />
          <span>Performance Optimization</span>
        </div>

        <div class="d-flex align-items-center gap-3">
          <SparklesIcon size="20" class="text-indigo-400" />
          <span>SSR Applications</span>
        </div>

        <div class="d-flex align-items-center gap-3">
          <SparklesIcon size="20" class="text-indigo-400" />
          <span>Platform Integrations</span>
        </div>

        <div class="d-flex align-items-center gap-3">
          <SparklesIcon size="20" class="text-indigo-400" />
          <span>Scalable Systems</span>
        </div>

        <div class="d-flex align-items-center gap-3">
          <SparklesIcon size="20" class="text-indigo-400" />
          <span>AI Tools</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { SparklesIcon } from 'lucide-vue-next';

export default {
  name: 'Marquee',
  components: {
    SparklesIcon
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