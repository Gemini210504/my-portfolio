<script setup>
import { Menu, X, Github, Linkedin, Facebook } from "lucide-vue-next";
import { ref } from "vue";

const isMobileMenuOpen = ref(false);

const navLinks = [
  { name: "Home", href: "#" },
  { name: "Projects", href: "#projects" },
  { name: "Skills", href: "#skills" },
  { name: "Contact", href: "#contact" },
];

const socialLinks = [
  {
    name: "Github",
    href: "https://github.com/Gemini210504",
    icon: Github,
  },
  {
    name: "Linkedin",
    href: "https://www.linkedin.com/in/leang-chhengleap-bb1a8039a?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app",
    icon: Linkedin,
  },
  {
    name: "Facebook",
    href: "https://www.facebook.com/share/1BJvV9YygQ/",
    icon: Facebook,
  },
];

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value;
};
</script>

<template>
  <nav class="nav-wrapper">
    <div class="glass nav-container">
      <div class="logo">
        <span class="gradient-text uppercase">Leang Chhengleap</span>
      </div>

      <!-- Desktop Nav -->
      <ul class="nav-links">
        <li v-for="link in navLinks" :key="link.name">
          <a :href="link.href">{{ link.name }}</a>
        </li>
      </ul>

      <!-- Social Icons -->
      <div class="social-icons">
        <a
          v-for="social in socialLinks"
          :key="social.name"
          :href="social.href"
          :aria-label="social.name"
          target="_blank"
          rel="noopener noreferrer"
        >
          <component :is="social.icon" :size="20" />
        </a>
      </div>

      <!-- Mobile Toggle -->
      <button
        class="mobile-toggle"
        @click="toggleMobileMenu"
        aria-label="Toggle menu"
      >
        <Menu v-if="!isMobileMenuOpen" />
        <X v-else />
      </button>
    </div>

    <!-- Mobile Menu -->
    <Transition name="fade">
      <div v-if="isMobileMenuOpen" class="glass mobile-menu">
        <ul class="mobile-nav-links">
          <li v-for="link in navLinks" :key="link.name">
            <a :href="link.href" @click="isMobileMenuOpen = false">{{
              link.name
            }}</a>
          </li>
        </ul>
      </div>
    </Transition>
  </nav>
</template>

<style scoped>
.nav-wrapper {
  position: fixed;
  top: 1.5rem;
  left: 50%;
  transform: translateX(-50%);
  width: 90%;
  max-width: 1200px;
  z-index: 1000;
}

.nav-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.75rem 2rem;
  border-radius: 50px;
}

.logo {
  font-family: var(--font-heading);
  font-weight: 800;
  font-size: 1.25rem;
  letter-spacing: -0.02em;
}

.nav-links {
  display: flex;
  gap: 2rem;
}

.nav-links a {
  font-size: 0.9rem;
  font-weight: 500;
  color: var(--text-secondary);
}

.nav-links a:hover {
  color: var(--text-primary);
}

.social-icons {
  display: flex;
  gap: 1.25rem;
  align-items: center;
}

.social-icons a {
  color: var(--text-secondary);
  display: flex;
  align-items: center;
}

.social-icons a:hover {
  color: var(--accent-color);
  transform: translateY(-2px);
}

.mobile-toggle {
  display: none;
  background: none;
  border: none;
  color: var(--text-primary);
  cursor: pointer;
}

.mobile-menu {
  position: absolute;
  top: calc(100% + 1rem);
  left: 0;
  right: 0;
  padding: 1.5rem;
  border-radius: var(--border-radius);
  text-align: center;
}

.mobile-nav-links {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.fade-enter-active,
.fade-leave-active {
  transition:
    opacity 0.3s ease,
    transform 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

@media (max-width: 768px) {
  .nav-links,
  .social-icons {
    display: none;
  }

  .mobile-toggle {
    display: block;
  }

  .nav-container {
    padding: 0.75rem 1.5rem;
  }
}
</style>
