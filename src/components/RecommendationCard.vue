<template>
    <div class="d-flex testimonial-flex position-relative px-5 mx-5 justify-content-center align-items-center testimonial-text testimonial-card">
        <div class="w-75">
            <small class="d-block text-center"><SvgIcon name="QuoteLeft" size="20" class="me-2"/>{{ recommendation.recommendation }}</small>
            <p class="text-center mt-3 fw-bold fs-5">-{{ recommendation.name }} <a :href="recommendation.profileLink" target="_blank" rel="noopener noreferrer"><SvgIcon name="ExternalLinkIcon" size="15" stroke-width="3" class="mb-1 cursor-pointer external-link-icon"/></a></p>
            <cite class="d-block text-center text-xs">{{ recommendation.relationship }}</cite>
        </div>
    </div>
</template>
<script>
import SvgIcon from './SvgIcon.vue';
export default {
    name: 'RecommendationsCard',
    components: {
        SvgIcon
    },
    props: {
        recommendation: {
            type: Object,
            required: true
        }
    }
}
</script>
<style >
.testimonial-text{
    font-family: "Space Mono", monospace;
    font-weight: 400;
}
.text-xs{
    font-size: 0.75rem;
}
.cursor-pointer{
    cursor: pointer;
}
.testimonial-card{
    min-height: 320px;
}
.external-link-icon:hover{
   transform: translateY(-3px);
}
</style>