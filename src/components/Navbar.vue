<template>
  <header class="position-relative z-1 mx-auto px-4 py-4 d-flex justify-content-between align-items-start" style="max-width: 1280px;">
    <div class="fs-2 fw-bold tracking-tighter border-bottom border-dark border-2 pb-1">
      it's me
    </div>

    <nav class="d-flex gap-5 text-sm">
      <a v-for="(item, i) in navItems" 
         :key="i" 
         :href="item.href" 
         class="group text-end d-none d-md-block text-decoration-none">
        <div class="d-flex align-items-center justify-content-end gap-1 fw-bold text-dark group-hover-zinc transition-all">
          {{ item.label }}
          <SvgIcon name="ArrowUpRightIcon" size="12" />
        </div>
        <div class="text-uppercase text-zinc-500 font-medium" style="font-size: 10px;">
          {{ item.sub }}
        </div>
      </a>
    </nav>
  </header>
</template>

<script>
import { ArrowUpRightIcon } from 'lucide-vue-next';
import SvgIcon from './SvgIcon.vue';
export default {
  name: 'Navbar',
  components: {
    SvgIcon
  },
  data() {
    return {
      navItems: [
        { label: 'My Projects', sub: 'See all work', href: '#projects' },
        { label: 'About Me', sub: 'Learn about me', href: '#experience' },
        { label: 'Contact me', sub: 'aryantnigam@gmail.com', href: 'mailto:aryantnigam@gmail.com' }
      ]
    };
  }
}
</script>

<style scoped>
.group-hover-zinc:hover {
  color: var(--zinc-500) !important;
}
</style>
