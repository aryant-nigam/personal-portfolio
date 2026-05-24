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
           Testimonials
        </div>

        <h2
          class="display-3 fw-bold text-uppercase lh-1"
          style="letter-spacing: -0.05em;"
        >
          A WORK <br />
          THAT SPEAKS
        </h2>
      </div>
      <div class="col-lg-4">
        <p class="text-secondary fs-6 lh-lg mb-0">
            More than building products — creating meaningful relationships and impact.
        </p>
      </div>
    </div>

    <!--RECOMMENDATIONS CAROUSEL-->
    <div id="carouselExampleInterval" class="carousel slide" data-bs-ride="carousel">
        <div class="carousel-inner h-100" style="min-height: max-content;">
            <div v-for="(recommendation, index) in recommendations" :key="index" class="carousel-item h-100" :class="{active: index === 0}" data-bs-interval="4000">
                <RecommendationCard :recommendation="recommendation"/>
            </div>
        </div>
        <button class="carousel-control-prev pe-lg-5 pe-md-4 pe-2" type="button" data-bs-target="#carouselExampleInterval" data-bs-slide="prev">
            <SvgIcon name="ChevronLeft" size="36" stroke-width="3" class="text-dark" />
            <span class="visually-hidden">Previous</span>
        </button>
        <button class="carousel-control-next ps-lg-5 ps-md-4 ps-2" type="button" data-bs-target="#carouselExampleInterval" data-bs-slide="next">
            <SvgIcon name="ChevronRight" size="36" stroke-width="3"  class="text-dark" />
            <span class="visually-hidden">Next</span>
        </button>
    </div>
  </section>
</template>

<script>
import recommendationsData from '../data/recommendations.json';
import RecommendationCard from './RecommendationCard.vue';
import SvgIcon from './SvgIcon.vue';
export default {
  name: 'Recommendations',

  components: {
    RecommendationCard,
    SvgIcon
  },

  data() {
    return {
      recommendations: recommendationsData,
      colorPalette: ['#60a5fa', '#6ee7b7', '#fef08a', '#fdba74', '#f472b6']
    };
  },

  computed: {
   
  },

   methods: {
    getInitials(name) {
      return name
        .split(' ')
        .map(word => word[0])
        .join('')
        .slice(0, 2)
        .toUpperCase();
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

</style>