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
      <Skills />
      <Recommendations />
      <Contact />
    </main>

   
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
import Skills from './components/Skills.vue';
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
    Skills,
    Recommendations,
    Contact,
    Footer
  }
}
</script>
