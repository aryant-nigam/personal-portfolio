<template>
  <div class="min-vh-100 position-relative overflow-x-hidden">
    <Background />

    <Navbar />

    <main>
      <Hero />
      <Marquee />
      <Socials />
      <Experience />
      <Projects />
      <Services />
      <Recommendations />
      <Contact />
    </main>

    <!-- Footer / Experience section can be added here if needed based on reference -->
    <Footer />
  </div>
</template>

<script>
import Background from './components/Background.vue';
import Navbar from './components/Navbar.vue';
import Hero from './components/Hero.vue';
import Marquee from './components/Marquee.vue';
import Socials from './components/Socials.vue';
import Experience from './components/Experience.vue';
import Projects from './components/Projects.vue';
import Services from './components/Services.vue';
import Recommendations from './components/Recommendations.vue';
import Contact from './components/Contact.vue';
import Footer from './components/Footer.vue';

export default {
  name: 'App',
  components: {
    Background,
    Navbar,
    Hero,
    Marquee,
    Socials,
    Experience,
    Projects,
    Services,
    Recommendations,
    Contact,
    Footer
  }
}
</script>
