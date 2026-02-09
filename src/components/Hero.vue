<script setup>
import { ArrowRight, ChevronDown } from "lucide-vue-next";
import { onMounted } from "vue";
import gsap from "gsap";
import Leap from "../assets/images/leap.jpg";

onMounted(() => {
  const tl = gsap.timeline();

  // Text content reveal
  tl.from(".hero-content h1", {
    y: 50,
    opacity: 0,
    duration: 0.8,
    ease: "power3.out",
  })
    .from(
      ".hero-content p",
      {
        y: 30,
        opacity: 0,
        duration: 0.8,
        ease: "power3.out",
      },
      "-=0.4",
    )
    .from(
      ".hero-actions",
      {
        y: 20,
        opacity: 0,
        duration: 0.8,
        ease: "power3.out",
      },
      "-=0.4",
    );

  // Profile image reveal
  gsap.from(".hero-image-container", {
    x: 100,
    opacity: 0,
    duration: 1.2,
    ease: "power4.out",
    delay: 0.5,
  });

  // Floating animation
  gsap.to(".profile-image-wrapper", {
    y: -20,
    duration: 2,
    repeat: -1,
    yoyo: true,
    ease: "sine.inOut",
  });

  // Mouse tracking parallax
  const hero = document.querySelector(".hero");
  const image = document.querySelector(".profile-image");

  hero.addEventListener("mousemove", (e) => {
    const { clientX, clientY } = e;
    const { innerWidth, innerHeight } = window;

    const xPos = (clientX / innerWidth - 0.5) * 40;
    const yPos = (clientY / innerHeight - 0.5) * 40;

    gsap.to(image, {
      x: xPos,
      y: yPos,
      duration: 1,
      ease: "power2.out",
    });
  });
});
</script>

<template>
  <section class="hero section">
    <div class="hero-container">
      <div class="hero-content">
        <h1 class="display-title">
          Building Digital <br />
          <span class="gradient-text">Experiences</span> that Matter
        </h1>
        <p class="hero-subtitle">
          I'm a Full Stack Developer passionate about creating beautiful,
          performant, and user-centric applications. Let's build something
          amazing together.
        </p>

        <div class="hero-actions">
          <a :href="'#projects'" class="btn btn-primary">
            View Projects <ArrowRight :size="18" />
          </a>
          <a :href="'#contact'" class="btn btn-secondary"> Contact Me </a>
        </div>
      </div>

      <div class="hero-image-container">
        <div class="profile-image-wrapper">
          <div class="image-border"></div>
          <img
            :src="Leap"
            alt="Leang Chhengleap Profile"
            class="profile-image"
          />
          <div class="experience-badge glass">
            <!-- <span class="badge-number">3+</span> -->
            <span class="badge-text">Junior Developer</span>
          </div>
        </div>
      </div>
    </div>

    <div class="scroll-indicator">
      <ChevronDown :size="32" class="bounce" />
    </div>

    <!-- Background Decor -->
    <div class="blob blob-1"></div>
    <div class="blob blob-2"></div>
  </section>
</template>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
}

.hero-container {
  display: flex;
  align-items: center;
  gap: 4rem;
  z-index: 1;
}

.hero-content {
  flex: 1.2;
}

.hero-image-container {
  flex: 0.8;
  display: flex;
  justify-content: center;
  align-items: center;
}

.profile-image-wrapper {
  position: relative;
  width: 400px;
  height: 480px;
}

.image-border {
  position: absolute;
  top: 20px;
  left: 20px;
  right: -20px;
  bottom: -20px;
  border: 2px solid var(--accent-color);
  border-radius: 20px;
  z-index: 0;
}

.profile-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 20px;
  position: relative;
  z-index: 1;
  box-shadow: 20px 20px 50px rgba(0, 0, 0, 0.5);
  filter: grayscale(20%) contrast(1.1);
}

.experience-badge {
  position: absolute;
  bottom: 0;
  left: -40px;
  padding: 1.5rem;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  z-index: 2;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.badge-number {
  font-size: 2rem;
  font-weight: 800;
  color: var(--accent-color);
  line-height: 1;
}

.badge-text {
  font-size: 0.8rem;
  font-weight: 600;
  color: var(--text-secondary);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.display-title {
  font-size: clamp(2.5rem, 8vw, 4.5rem);
  margin-bottom: 1.5rem;
  line-height: 1.1;
  letter-spacing: -0.02em;
}

.hero-subtitle {
  font-size: clamp(1.1rem, 2vw, 1.25rem);
  color: var(--text-secondary);
  max-width: 600px;
  margin-bottom: 2.5rem;
}

.hero-actions {
  display: flex;
  gap: 1rem;
}

.btn {
  padding: 0.8rem 2rem;
  border-radius: 50px;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 0.75rem;
  transition: var(--transition-smooth);
}

.btn-primary {
  background: var(--accent-gradient);
  color: white;
  border: none;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 20px rgba(99, 102, 241, 0.3);
}

.btn-secondary {
  background: var(--glass-bg);
  border: 1px solid var(--glass-border);
  color: var(--text-primary);
  backdrop-filter: blur(5px);
}

.btn-secondary:hover {
  background: var(--glass-border);
  transform: translateY(-2px);
}

.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  color: var(--text-secondary);
}

.bounce {
  animation: bounce 2s infinite;
}

@keyframes bounce {
  0%,
  20%,
  50%,
  80%,
  100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-10px);
  }
  60% {
    transform: translateY(-5px);
  }
}

/* Background Blobs */
.blob {
  position: absolute;
  z-index: -1;
  filter: blur(80px);
  border-radius: 50%;
  opacity: 0.15;
}

.blob-1 {
  width: 400px;
  height: 400px;
  background: var(--accent-color);
  top: -100px;
  right: -100px;
}

.blob-2 {
  width: 300px;
  height: 300px;
  background: #a855f7;
  bottom: 50px;
  left: -50px;
}

@media (max-width: 1024px) {
  .hero-container {
    gap: 2rem;
  }
  .profile-image-wrapper {
    width: 320px;
    height: 400px;
  }
}

@media (max-width: 768px) {
  .hero-container {
    flex-direction: column;
    text-align: center;
    padding-top: 4rem;
  }
  .hero-actions {
    flex-direction: row;
    justify-content: center;
  }
  .hero-image-container {
    order: -1;
  }
  .profile-image-wrapper {
    width: 280px;
    height: 350px;
  }
  .experience-badge {
    left: 50%;
    transform: translateX(-50%);
    bottom: -20px;
  }
}

@media (max-width: 480px) {
  .hero-actions {
    flex-direction: column;
  }
}
</style>
