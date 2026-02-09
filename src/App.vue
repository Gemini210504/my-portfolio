<script setup>
import { onMounted } from "vue";
import gsap from "gsap";
import { Toaster } from "vue-sonner";
import Navbar from "./components/Navbar.vue";
import Hero from "./components/Hero.vue";
import PortfolioGrid from "./components/PortfolioGrid.vue";
import Skills from "./components/Skills.vue";
import Contact from "./components/Contact.vue";
import EducationHistory from "./components/EducationHistory.vue";

onMounted(() => {
  gsap.from(".app-container", {
    opacity: 0,
    duration: 1,
    ease: "power2.out",
  });
});
</script>

<template>
  <div class="app-container">
    <Toaster position="top-right" richColors />
    <Navbar />
    <main>
      <Hero />
      <PortfolioGrid />
      <EducationHistory />
      <Skills />
      <Contact />
    </main>
    <footer class="glass footer">
      <div class="footer-content">
        <p>&copy; 2026 Modern Portfolio. Built with Vue & GSAP.</p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.app-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

main {
  flex: 1;
}

.footer {
  margin-top: auto;
  padding: var(--spacing-md);
  text-align: center;
  border-right: none;
  border-left: none;
  border-bottom: none;
  border-radius: 0;
}

.footer-content p {
  color: var(--text-secondary);
  font-size: 0.9rem;
}
</style>
