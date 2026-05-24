<template>
  <section
    id="projects"
    class="container-xl py-5 px-4 position-relative"
  >
    <!-- HEADER -->
    <div class="row align-items-end gy-4 mb-5">

      <div class="col-lg-8">
        <div
          class="d-flex align-items-center gap-3 text-uppercase fw-bold small text-secondary mb-3"
          style="letter-spacing: 0.18em;"
        >
          <div class="section-line"></div>
          Selected Works
        </div>

        <h2
          class="display-3 fw-bold text-uppercase lh-1"
          style="letter-spacing: -0.05em;"
        >
          FEATURED <br />
          PROJECTS
        </h2>
      </div>

      <div class="col-lg-4">
        <p class="text-secondary fs-6 lh-lg mb-0">
          A collection of tools, AI workflows, products,
          and experiments built with performance and
          clean user experience in mind.
        </p>
      </div>

    </div>

    <!-- PROJECT STACK -->
    <div class="project-stack position-relative pt-5">

      <!-- STACK BACKGROUND -->
      <div
        class="stack-layer position-absolute start-50 translate-middle-x rounded-5 bg-light border opacity-50"
        style="width: 90%; height: 90%; top: 0.4rem; z-index: 0;"
      ></div>

      <div
        class="stack-layer position-absolute start-50 translate-middle-x rounded-5 bg-light border opacity-75"
        style="width: 95%; height: 90%; top: 1.7rem; z-index: 1;"
      ></div>

      <!-- CARD -->
      <transition name="slide-fade" mode="out-in">
        <div
          :key="activeProjectIndex"
          class="project-card bg-white border rounded-5 shadow-sm p-4 p-lg-5 d-flex flex-column position-relative"
        >

          <!-- TOP -->
          <div
            class="d-flex justify-content-between align-items-start flex-wrap gap-4 mb-5"
          >

            <!-- TAGS -->
            <div class="d-flex flex-wrap gap-2">

              <span
                v-for="tag in currentProject.tags"
                :key="tag"
                class="badge rounded-pill bg-light border text-dark px-3 py-2 text-uppercase"
              >
                {{ tag }}
              </span>

            </div>

            <!-- NUMBER -->
            <div
              class="project-number d-flex align-items-center justify-content-center rounded-circle border fw-bold"
            >
              {{
                activeProjectIndex + 1 < 10
                  ? `0${activeProjectIndex + 1}`
                  : activeProjectIndex + 1
              }}
            </div>

          </div>

          <!-- TITLE -->
          <h2
            class="display-3 fw-bold lh-1 mb-4"
            style="letter-spacing: -0.05em;"
          >
            {{ currentProject.title }}
          </h2>

          <!-- DESCRIPTION -->
          <small class="text-secondary lh-lg mb-5 col-lg-10">
            {{ currentProject.description }}
          </small>

          <!-- STACK -->
          <p class="font-monospace text-secondary fw-semibold mb-5">
            {{ currentProject.stack }}
          </p>

          <!-- FOOTER -->
          <div
            class="d-flex justify-content-between align-items-center flex-wrap gap-4 mt-auto"
          >

            <div class="d-flex gap-3 flex-wrap">

              <a
                :href="currentProject.previewLink"
                target="_blank"
                class="btn btn-dark rounded-pill px-4 py-3 fw-semibold"
              >
                View Project
              </a>

              <a
                v-if="currentProject.sourceLink"
                :href="currentProject.sourceLink"
                target="_blank"
                class="btn btn-outline-dark rounded-pill px-4 py-3 fw-semibold"
              >
                Source
              </a>

            </div>

            <div class="text-secondary fw-semibold">
              {{ activeProjectIndex + 1 }}
              /
              {{ projects.length }}
            </div>

          </div>

        </div>
      </transition>

    </div>

    <!-- NAVIGATION -->
    <div
      class="d-flex justify-content-center gap-3 mt-4 position-relative"
      style="z-index: 10;"
    >

      <button
        type="button"
        class="btn btn-dark rounded-circle d-flex align-items-center justify-content-center nav-btn"
        style="width: 60px; height: 60px;"
        @click="previousProject"
      >
        <SvgIcon name="ChevronLeft" size="36" stroke-width="3" />
      </button>

      <button
        type="button"
        class="btn btn-dark rounded-circle d-flex align-items-center justify-content-center nav-btn"
        style="width: 60px; height: 60px;"
        @click="nextProject"
      >
        <SvgIcon name="ChevronRight" size="36" stroke-width="3" />
      </button>

    </div>

  </section>
</template>

<script>
import projectsData from '../data/projects.json';
import SvgIcon from './SvgIcon.vue';

export default {
  name: 'Projects',

  components: {
    SvgIcon
  },

  data() {
    return {
      projects: projectsData,
      activeProjectIndex: 0
    };
  },

  computed: {
    currentProject() {
      return this.projects[this.activeProjectIndex];
    }
  },

  methods: {
    nextProject() {
      this.activeProjectIndex =
        (this.activeProjectIndex + 1) % this.projects.length;
    },

    previousProject() {
      this.activeProjectIndex =
        (this.activeProjectIndex - 1 + this.projects.length) %
        this.projects.length;
    }
  }
};
</script>

<style scoped>
.section-line {
  width: 40px;
  height: 1px;
  background: currentColor;
}

.project-card {
  min-height: 70vh;
  z-index: 5;
}

.project-number {
  width: 80px;
  height: 80px;
  font-size: 1.4rem;
}

.nav-btn {
  transition:
    transform 0.2s ease,
    opacity 0.2s ease;
}

.nav-btn:hover {
  transform: translateY(-3px);
  opacity: 0.9;
}

/* TRANSITION */

.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all 0.35s ease;
}

.slide-fade-enter-from {
  opacity: 0;
  transform: translateY(24px);
}

.slide-fade-leave-to {
  opacity: 0;
  transform: translateY(-24px);
}
</style>