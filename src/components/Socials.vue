<template>
  <div class="position-relative z-1 mx-auto px-4 py-5 d-flex flex-column flex-md-row justify-content-between align-items-center gap-4 border-bottom border-zinc-100" style="max-width: 1280px;">
    <div class="d-flex align-items-center gap-5">
      <a :href="userData.github" target="_blank" class="d-flex align-items-center gap-2 text-xs fw-bold text-uppercase text-black text-decoration-none transition-all socials">
        <SvgIcon name="GithubIcon" size="18" stroke-width="2"/> GITHUB
      </a>
      <a :href="userData.linkedin" target="_blank" class="d-flex align-items-center gap-2 text-xs fw-bold text-uppercase text-black text-decoration-none transition-all socials">
        <SvgIcon name="LinkedinIcon" size="18" stroke-width="2" /> LINKEDIN
      </a>
    </div>
    <div class="d-flex align-items-center gap-3 text-xs fw-bold text-black">
      <SvgIcon name="MailIcon" size="18" stroke-width="2" /> {{ userData.email.toUpperCase() }}
    </div>
  </div>
</template>

<script>
import SvgIcon from './SvgIcon.vue';
export default {
  name: 'Socials',
  components: {
    SvgIcon
  },
  data() {
    return {
      userData: {
        email: "aryantnigam@gmail.com",
        github: "https://github.com/aryant-nigam",
        linkedin: "https://shorturl.at/giaS9"
      }
    };
  }
}
</script>

<style scoped>
.socials:hover { color: var(--zinc-600) !important; } 
</style>
