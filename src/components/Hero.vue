<template>
  <section class="position-relative z-1 mx-auto px-4 pt-4 pb-5 row align-items-center g-5" style="max-width: 1280px; min-height: 80vh;">
    <div class="col-lg-7 d-flex flex-column gap-5">
      <div class="d-flex flex-column gap-4">
        <div class="d-flex align-items-center gap-3 fs-2">
          <span class="animate-wave">👋</span>
          <span class="fw-light text-zinc-500">Hello!</span>
          <h1 class="display-4 fw-black tracking-tight m-0">I'm Aryant</h1>
        </div>

        <div class="d-flex align-items-center gap-4 py-2 border-top border-bottom border-zinc-100 w-fit pe-5">
          <div class="bg-zinc-300" style="height: 1px; width: 48px;"></div>
          <span class="fs-4 fw-medium text-zinc-600 text-uppercase tracking-widest">{{ userData.role }}</span>
          <SvgIcon name="SparklesIcon" size="20" class="text-zinc-900 fill-zinc-900" />
        </div>

        <p class="text-zinc-500 fs-5 leading-relaxed m-0" style="max-width: 450px;">
          {{ userData.description }}
        </p>
      </div>

      <ul class="list-unstyled d-flex flex-column gap-3">
        <li v-for="(text, i) in features" :key="i" class="d-flex align-items-center gap-3 text-sm fw-bold text-zinc-700">
          <SvgIcon name="CheckIcon" size="16" class="text-zinc-900" />
          {{ text }}
        </li>
      </ul>

      <div class="d-flex align-items-center gap-4">
        <button @click="scrollToContact" class="btn btn-dark px-5 py-3 rounded-pill fw-bold shadow-lg">
          Let's Talk
        </button>
        <a
          href="/files/aryant_nigam_fullstack_web_developer_resume.pdf"
          download
          class="btn bg-transparent border-0 border-bottom border-2 border-zinc-200 rounded-0 px-0 pb-1 fw-bold d-flex align-items-center gap-2"
        >
          Download Resume
          <SvgIcon name="DownloadIcon" size="16" stroke-width="3" />
        </a>
      </div>
    </div>

    <!-- Right Side Content -->
    <div class="col-lg-5 d-flex d-lg-flex justify-content-center position-relative">
      <!-- Floating Badge 1 -->
      <div class="position-absolute top-0 start-0 translate-middle-y bg-white rounded-4 p-2 p-md-3 shadow-lg z-3 d-flex align-items-center gap-3" style="margin-top: 15%; margin-left: 5%; animation: bounce 3s infinite ease-in-out;">
        <div class="bg-dark rounded-circle d-flex align-items-center justify-content-center text-white" style="width: 1.5rem; height:1.5rem;">
          <SvgIcon name="CodeIcon" size="20" />
        </div>
        <div>
          <p class="mb-0 fw-bold tracking-tight">20+</p>
          <span class="text-zinc-500 small">Features Shipped</span>
        </div>
      </div>

      <!-- Main Profile Card -->
      <div class="profile-card rounded-5 overflow-hidden position-relative w-75 skew-y-1 z-2">
        <img src="/me.jpg" alt="Profile or Workspace" class="w-100 h-100" style="object-fit: cover;" />
      </div>

      <!-- Floating Badge 2 -->
      <div class="position-absolute bottom-0 end-0 bg-dark text-white rounded-4 p-2 p-md-3 shadow-lg z-3 d-flex align-items-center gap-3" style="margin-bottom: 10%; margin-right: 5%; animation: bounce 4s infinite ease-in-out 1s;">
        <div class="bg-white rounded-circle d-flex align-items-center justify-content-center text-dark" style="width: 1.5rem; height: 1.5rem;">
          <SvgIcon name="StarIcon" size="20" />
        </div>
        <div>
          <p class="mb-0 fw-bold tracking-tight">3 Years</p>
          <span class="text-white-50 small">Experience</span>
        </div>
      </div>
    </div>

  </section>
</template>

<script>
import SvgIcon from './SvgIcon.vue';
import { SparklesIcon, CheckIcon, DownloadIcon, CodeIcon, StarIcon } from 'lucide-vue-next';

export default {
  name: 'Hero',
  components: {
    SvgIcon,
    SparklesIcon,
    CheckIcon,
    DownloadIcon,
    CodeIcon,
    StarIcon
  },
  data() {
    return {
      userData: {
        role: "Full Stack Engineer",
        description: "Full-stack engineer building scalable web systems, cloud automations, APIs, and high-performance user experiences."
      },
      features: [
        'Code must be scalable',
        'Solve pain points elegantly',
        'Continuous testing & validation'
      ]
    };
  },
  methods: {
    scrollToContact() {
      const section = document.getElementById('contact');
      if (section) {
        section.scrollIntoView({ behavior: 'smooth' });
      }
    }
  }
}
</script>

<style scoped>
.fw-black { font-weight: 900; }
.w-fit { width: fit-content; }
.hover-black:hover { border-color: #000 !important; }
.text-xs { font-size: 11px; }
.fill-zinc-300 { fill: var(--zinc-300); }
</style>
